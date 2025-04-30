# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL

## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
## server

      import socket
      s = socket.socket()
      s.bind(('localhost', 9999))
      s.listen(1)
      print("Server listening...")
      conn, addr = s.accept()
      print(f"Connected to {addr}")

      while True:
          frames = conn.recv(1024).decode()
          if not frames:
              break

          print(f"Received frames: {frames}")
          ack_message = f"ACK for frames: {frames}"
          conn.send(ack_message.encode())

      conn.close()  
      s.close()  

## client 

      import socket
      c = socket.socket()
      c.connect(('localhost', 9999))

      size = int(input("Enter number of frames to send: "))
      l = list(range(size))  
      print("Total frames to send:", len(l))
      s = int(input("Enter Window Size: "))

      i = 0
      while True:
          while i < len(l):
              st = i + s
              frames_to_send = l[i:st]  
              print(f"Sending frames: {frames_to_send}")
              c.send(str(frames_to_send).encode())  

              ack = c.recv(1024).decode()  
              if ack:
                  print(f"Acknowledgment received: {ack}")
                  i += s  

          break
      c.close()  


## OUPUT

## server
![370846500-6cefbc06-b4c8-440f-8ce4-e9e9c35a4439](https://github.com/user-attachments/assets/1c3b173a-4ab1-43b1-ba27-c487876f5396)

## client 
![370846589-70dfb06d-d87f-4899-ac58-b658844bf28c](https://github.com/user-attachments/assets/e7c72eb9-b40d-49ec-afe7-5068a6ac39aa)


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
