# music-control-using-face-detection
#With the help of python programming we can control the music playing on vlc media player using face detection.
#here is its code
import cv2
import vlc
m=vlc.MediaPlayer(r'E:\songs\audios\01 Awargi - Love Games - 190Kbps.mp3')
m.play()
cam=cv2.VideoCapture(0)
fd=cv2.CascadeClassifier(r'G:\Python\Lib\site-packages\cv2\data\haarcascade_frontalface_alt.xml')
flag=0
while True:
    r,i=cam.read()
    j=cv2.cvtColor(i,cv2.COLOR_BGR2GRAY)
    face=fd.detectMultiScale(j,1.3,7)
    L=len(face)
    print(face,L)
    if(L>0):
        for(x,y,w,h) in face:
            cv2.rectangle(i,(x,y),(x+w,y+h),(0,0,0),-1)
            m.play()
            m.audio_set_volume(100-int((w+h)/1000))
            flag=1
    elif(flag==1):
        m.pause()
        flag=0

    cv2.imshow('image',i)
    k=cv2.waitKey(5)
    if(k==ord('q')):
        cv2.destroyAllWindows()
        break
