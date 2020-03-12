# 网络编程

### TCP网络编程

#### Server端

1. 首先创建ServerSocket，可设置好端口号
2. 接收客户端的连接
3. 通过Socket进行收发消息
4. 与客户端断开连接

```text
		// 1、创建ServerSocket，看成：开启服务器 ，需要指定一个端口号，监听是否有客户端来连接
		ServerSocket ss = new ServerSocket(9090);
		
		while(true){
			System.out.println("等待您的链接....");
			// 2、等待客户端的连接，接收客户端的连接（
			// 如果没有人连接，那么这句代码会阻塞）
			// 一旦有客户端连接成功，那么就会产生一个Socket对象，
			// 专门负责和这个客户端通信
			Socket socket = ss.accept();
			
			System.out.println(socket.getInetAddress().getHostAddress()+"连接成功");
			
			// 3、可以接收消息，或发生消息
			// 例如：先发：“欢迎登陆”
			// 在接收消息
			
			// 发消息：输出流，OutputStream
			OutputStream output = socket.getOutputStream();
			output.write("欢迎".getBytes());
			socket.shutdownOutput();
			
			// 收消息
			InputStream is = socket.getInputStream();
			
			byte[] data = new byte[1024];
			int len;
			StringBuilder sb = new StringBuilder();
			while((len= is.read(data)) !=-1){
				sb.append(new String(data,0,len));
			}
			System.out.println("服务器收到的消息：" + sb);
			
			// 4、关闭连接 只是与某个客户端断开
			socket.close();
		}
		
		//5、服务器关闭
		ss.close();
```

#### Client端

1. 先与服务器端建立连接，通过建立一个Socket,要指定服务器IP与端口
2. 通过socket收发消息
3. 与服务器端口连接

```text
		// 1、连接服务器
		Socket socket = new Socket("192.168.1.22",9999);
		
		OutputStream out = socket.getOutputStream();
		
		// 2，从键盘输入给服务器发送
		Scanner input = new Scanner(System.in);
		while(true){
			System.out.println("输入要发送的内容：");
			String info = input.nextLine();
			
			if("byebye".equals(info)){
				break;
			}
			
			//给服务器发送
			out.write((info+"\n").getBytes());
		}
		
		//3、断开
		socket.close();
```

### UDP网络编程

#### 发送端

1. 创建一个DatagramSocket
2. 准备发送的数据，并且进行打包
3. 通过DatagramSocket的send数据包
4. 关闭

```text
   DatagramSocket ds = new DatagramSocket();
		
		//2、把数据打包成一个数据报，包
		String str = "UDP";
		byte[] bytes = str.getBytes();
		InetAddress ip = InetAddress.getByName("192.168.1.22");
		DatagramPacket dp = new DatagramPacket(bytes, bytes.length, ip,8989);
		
		//3、通过socket发送出去
		ds.send(dp);
		System.out.println("发送完毕");
		
		//4、释放资源
		ds.close();
```

#### 接收端

1. 创建一个DatagramSocket，需要指定监听的端口号
2. 准备一个DatagramPacket,用来接收数据
3. 通过DatagramSocket的recevice数据包
4. 拆解数据，通过DatagramPacket对象的getData\(\)方法获取数据
5. 关闭

```text
		//1、创建Socket
		DatagramSocket ds = new DatagramSocket(8989);//为它指定一个端口号，在端口号一直监听着
		
		//2、先创建一个数据报等着
		byte[] data = new byte[1024];
		DatagramPacket dp  = new DatagramPacket(data, data.length);
		
		//3、准备接受数据，从socket中接收数据，如果此时没有数据，这句代码会阻塞
		ds.receive(dp);
		
		//4、拆出数据
		String str = new String(dp.getData(),0,dp.getLength());
		System.out.println("收到的数据是：" + str);
		
		//5、关闭
		ds.close();
```

