[toc]
# GUI
## 1.GUI概述
## 2.布局（frame）
创建图形化界面的步骤  
1.创建frame窗体  
2.对窗体进行基本设置。比如大小，位置，布局  
3.定义组件  
4.将组件通过窗体的add方法添加到窗体中。  
5.让窗体显示，通过setVisible(true) 

    package Demo;
    import java.awt.*;
    public class AwtDemo {
    	public static void main(String[] args) {
    		Frame f=new Frame("my awt");
    		f.setSize(500, 500);//宽高
    		f.setLocation(300, 200);//位置
    		f.setLayout(new FlowLayout());//设置流式布局
    		Button b=new Button("我是一个按钮");//系统默认有一个边界式布局，没有指定东南西北中，所以会出现居中填充,按钮超级大
    		f.add(b);
    		f.setVisible(true);//显示窗口
    	}
    }
## 3.事件监听机制
1.事件源(组件)  
2事件(Event)  
3监听器(Listener)  
4事件处理(引发事件后处理方式)  

事件源：就是awt包或者swing包中的那些图形界面组件  

事件：每一个事件源都有自己特有的对应事件和 共性事件  

监听器：将可以触发某一个事件的动作都已经封装到了监听器中。

以上三者，在Java中都已经定义好了
直接获取其对象来用就可以了。

我们要做的事情是，就是对产生的动作进行处理
## 4.窗体事件

    package Demo;
    import java.awt.*;
    import java.awt.event.*;
    public class AwtDemo {
    	public static void main(String[] args) {
    		Frame f=new Frame("my awt");
    		f.setSize(500, 500);//宽高
    		f.setLocation(300, 200);//位置
    		f.setLayout(new FlowLayout());//设置流式布局
    		Button b=new Button("我是一个按钮");//系统默认有一个边界式布局，没有指定东南西北中，所以会出现居中填充,按钮超级大
    		f.add(b);
    		f.setVisible(true);//显示窗口
    		f.addWindowListener(new WindowAdapter() {
    			public void windowClosing(WindowEvent e) {
    				System.out.println("我关");
    				System.exit(0);
    			}
    			public void windowActivated(WindowEvent e) {
    				System.out.println("我活了！");
    			}
    			public void windowOpened(WindowEvent e) {
    				System.out.println("我被打开了");
    			}
    		});
    	}
    }
## 5.Action事件
    package Demo;
    import java.awt.*
    public class FrameDemo {
    	//定义该图形中所需的组件的引用
    	private Frame f;
    	private Button but;
    	
    	FrameDemo01()
    	{
    		init();
    	}
    	
    	public void init()
    	{
    		f=new Frame("my frame");
    		
    		//对frame进行基本设置
    		f.setBounds(300, 100, 600, 500);
    		f.setLayout(new FlowLayout());
    		
    		but=new Button("my button");
    		
    		//将组件添加到frame中
    		f.add(but);
    		
    		//加载一下窗体上的事件
    		myEvent();
    		
    		//显示窗体
    		f.setVisible(true);
    		
    	}
    	private void myEvent() {
    		f.addWindowListener(new WindowAdapter() {
    			public void windowClosing(WindowEvent e) {
    				System.exit(0);
    			}
    		});
    		
    		//让按钮具备退出程序的功能
    		/*
    		 * 按钮就是事件源
    		 * button的描述中，有支持一个特有的监听addActionListener
    		 */
    		but.addActionListener(new ActionListener() {
    			public void actionPerformed(ActionEvent e) {
    				System.out.println("退出，按钮干的");
    				System.exit(0);
    			}
    		});
    	}
    
    	public static void main(String[] args) {
    		// TODO Auto-generated method stub
    		new FrameDemo01();
    	}
    
    }
## 6.鼠标事件
    package Demo;
    import java.awt.*
    public class Demo01 {
    	    private Frame f;
    		private Button but;
    		Demo01(){
    			init();
    		}
    		public void init(){
    			f=new Frame("my frame");
    			f.setBounds(300, 100, 600, 500);
    			f.setLayout(new FlowLayout());
    			but=new Button("my button");
    			f.add(but);
    			myEvent();
    			f.setVisible(true);
    		}
    		
    		private void myEvent() {
    			f.addWindowListener(new WindowAdapter() {
    				public void windowClosing(WindowEvent e) {
    					System.exit(0);
    				}
    			});
    			
    			but.addActionListener(new ActionListener() {
    
    			
    				public void actionPerformed(ActionEvent arg0) {
    					System.out.println("action ok");   //注意：鼠标和键盘都可以触动按钮
    				}			                           //若用鼠标，先是mouseClicked
    			});
    			
    			but.addMouseListener(new MouseAdapter() {
    				private int count=1;
    				private int clickCount=1;
    				public void mouseEntered(MouseEvent w) {
    					System.out.println("鼠标进入该组件"+(count++));
    				}
    				
    				public void mouseClicked(MouseEvent e) {
    					if(e.getClickCount()==2)
    					System.out.println("双击动作"+count++);
    				}
    				
    			});
    		}
    	public static void main(String[] args) {
    		new Demo01();
    	}
    
    }
## 7.键盘事件
    package Demo;
    import java.awt.*
    import java.awt.event.*;
    public class Demo01 {
    	    private Frame f;
    		private Button but;
    		private TextField tf;
    		Demo01(){
    			init();
    		}
    		public void init(){
    			f=new Frame("my frame");
    			f.setBounds(300, 100, 600, 500);
    			f.setLayout(new FlowLayout());
    			
    			//设置文本框
    			tf=new TextField(20);//指定列数
    			
    			
    			but=new Button("my button");
    			
    			f.add(tf);
    			f.add(but);
    			myEvent();
    			f.setVisible(true);
    		}
    		
    		private void myEvent() {
    			f.addWindowListener(new WindowAdapter() {
    				public void windowClosing(WindowEvent e) {
    					System.exit(0);
    				}
    			});
    			
    			//给文本框添加键盘监听
    			tf.addKeyListener(new KeyAdapter() {
    				public void keyPressed(KeyEvent e) {
    					
    					int code=e.getKeyChar();
    					if(!(code>=KeyEvent.VK_0&&code<=KeyEvent.VK_9)) {
    						System.out.println(code+".....是非法的");
    						e.consume();//不按照默认的，不输出
    					}
    				}
    			});
    			
    			
    			
    			but.addActionListener(new ActionListener() {
    
    			
    				public void actionPerformed(ActionEvent arg0) {
    					
    					System.out.println("action ok");   //注意：鼠标和键盘都可以触动按钮
    				}			                           //若用鼠标，先是mouseClicked
    			});
    			
    			but.addMouseListener(new MouseAdapter() {
    				private int count=1;
    				private int clickCount=1;
    				public void mouseEntered(MouseEvent w) {
    					System.out.println("鼠标进入该组件"+(count++));
    				}
    			
    				public void mouseClicked(MouseEvent e) {
    					
    					if(e.getClickCount()==2)
    					System.out.println("双击动作"+count++);
    				}
    				
    			});
    			
    			//给but添加一个键盘监听器
    			but.addKeyListener(new KeyAdapter() {
    
    				public void keyPressed(KeyEvent e) {
    					//System.out.println(e.getKeyChar()+"........."+e.getKeyCode());
    					//打印标准的ASCLL码和键盘码
    					
    					//System.out.println(KeyEvent.getKeyText(e.getKeyCode())+"........."+e.getKeyCode());
    					//打印件键盘名和键盘码
    					
    					/*if(e.getKeyCode()==27)
    					if(e.getKeyCode()==KeyEvent.VK_ESCAPE)//按esc键退出
    						System.exit(0);*/
    					
    					if(e.isControlDown()&&e.getKeyCode()==KeyEvent.VK_ESCAPE)
    						System.out.println("ctrl+enter  is  run");//ctrl+enter
    				}
    				
    			});
    			
    			
    		}
    	public static void main(String[] args) {
    		
    		new Demo01();
    	}
    
    }
## 8.列出指定目录
    package Demo;
    
    import java.awt.*;
    import java.event.*;
    
    public class MyWindows {
    	private Frame f;
    	private TextField tf;
    	private Button but;
    	private TextArea ta;
    	
    	MyWindows(){
    		init();
    	}
    
    	public void init() {
    		f=new Frame("my windows");
    		f.setBounds(300, 100, 600, 500);
    		f.setLayout(new FlowLayout());
    		
    		tf=new TextField(60);
    		but=new Button("转到");
    		ta=new TextArea(25,70);
    		
    		f.add(tf);
    		f.add(but);
    		f.add(ta);
    		
    		myEvent();
    		f.setVisible(true);
    	}
    	private void myEvent() {
    		but.addActionListener(new ActionListener() {
    			
    		
    			public void actionPerformed(ActionEvent arg0) {
    				
    				String dirPath=tf.getText();
    				
    				File dir=new File(dirPath);
    				
    				if(dir.exists()&&dir.isDirectory()) {
    					String []names=dir.list();
    					for(String name:names)
    					{
    						ta.setText(name+"\r\n");
    					}
    				}
    				/*ta.setText(text);
    				//System.out.println(text);*/
    				//tf.setText("");//清空
    			}
    		});
    		
    		
    		f.addWindowListener(new WindowAdapter() {
    
    			
    			public void windowClosing(WindowEvent arg0) {
    				
    				System.exit(0);
    			}
    		});
    	}
    	
    	public static void main(String[] args) {
    		new MyWindows();
    	}
    
    }
## 9. 对话框Dialog
    package Demo;
    
    import java.awt.*;
    import java.io.*;
    import java,awt.event.*;
    
    public class MyWindows {
    	private Frame f;
    	private TextField tf;
    	private Button but;
    	private TextArea ta;
    	
    	
    	private Dialog d;
    	private Label lab;
    	private Button okBut;
    	
    	MyWindows(){
    		init();
    	}
    
    	public void init() {
    		f=new Frame("my windows");
    		f.setBounds(300, 100, 600, 500);
    		f.setLayout(new FlowLayout());
    		
    		tf=new TextField(60);
    		but=new Button("转到");
    		ta=new TextArea(25,70);
    		
    		d=new Dialog(f,"提示信息-self",true);
    		d.setBounds(400, 200, 240, 250);
    		d.setLayout(new FlowLayout());
    		lab=new Label();
    		okBut=new Button("确定");
    		
    		d.add(lab);
    		d.add(okBut);
    		
    		f.add(tf);
    		f.add(but);
    		f.add(ta);
    		
    		myEvent();
    		f.setVisible(true);
    	}
    	private void myEvent() {
    		okBut.addActionListener(new ActionListener() {
    			public void actionPerformed(ActionEvent arg0) {
    				d.setVisible(false);
    			}
    		});
    		
    		d.addWindowListener(new WindowAdapter() {
    
    			
    			public void windowClosing(WindowEvent arg0) {
    				
    				d.setVisible(false);
    			}
    		});
    		
    		tf.addKeyListener(new KeyAdapter() {
    			public void keyPressed(KeyEvent e) {
    				if(e.getKeyCode()==KeyEvent.VK_ENTER) {
    					showDir();
    				}
    			}
    		});
    	
    		but.addActionListener(new ActionListener() {	
    			
    			public void actionPerformed(ActionEvent arg0) {
    				
    				showDir();
    			}
    		});
    		
    		
    		f.addWindowListener(new WindowAdapter() {
    
    			
    			public void windowClosing(WindowEvent arg0) {
    				
    				System.exit(0);
    			}
    		});
    	}
    	
    	private void showDir() {
    		String dirPath=tf.getText();
    		
    		File dir=new File(dirPath);
    		
    		if(dir.exists()&&dir.isDirectory()) {
    			String []names=dir.list();
    			for(String name:names)
    			{
    				ta.setText(name+"\r\n");
    			}
    		}else {
    			String info="您输入的信息："+dirPath+"是错误的，请重输";
    			lab.setText(info);
    			d.setVisible(true);
    		}
    		/*ta.setText(text);
    		//System.out.println(text);*/
    		//tf.setText("");//清空
    	}
    	
    	public static void main(String[] args) {
    		// TODO Auto-generated method stub
    		new MyWindows();
    	}
    
    }
## 10.打开文件
    package Demo;
    
    import java.awt.*;
    import java.awt.event.*;
    import java.io.*;
    
    public class MyMenuDemo {
    	private Frame f;
    	private TextArea ta;
    	private MenuBar bar;
    	private Menu fileMenu;
    	private MenuItem openItem,saveItem,closeItem;
    	
    	private FileDialog openDia,saveDia;
    	
    	MyMenuDemo(){
    		init();
    	}
    	
    	public void init() {
    		f=new Frame("记事本");
    		f.setBounds(300, 100, 650, 500);
    		
    		bar=new MenuBar();
    		ta=new TextArea();
    
    		fileMenu=new Menu("文件");
    		
    		openItem=new MenuItem("打开");
    		saveItem=new MenuItem("保存");
    		closeItem=new MenuItem("退出");
    		
    		fileMenu.add(openItem);
    		fileMenu.add(saveItem);
    		fileMenu.add(closeItem);
    
    		bar.add(fileMenu);
    		
    		f.setMenuBar(bar);
    		
    		
    		openDia=new FileDialog(f,"打开",FileDialog.LOAD);//打开
    		saveDia=new FileDialog(f,"保存",FileDialog.SAVE);//打开
    		
    		
    		f.add(ta);
    		MyEvent();
    		f.setVisible(true);
    	}
    	
    	private void MyEvent() {
    		openItem.addActionListener(new ActionListener() {
    			
    			public void actionPerformed(ActionEvent e) {
    				openDia.setVisible(true);
    				String dirPath=openDia.getDirectory();
    				String fileName=openDia.getFile();
    				System.out.println(dirPath+"......"+fileName);
    				if(dirPath==null||fileName==null)
    					return;
    				ta.setText("");
    				File file=new File(dirPath,fileName);
    				try {
    					BufferedReader bufr=new BufferedReader(new FileReader(file));
    					String line=null;
    					
    					while((line=bufr.readLine())!=null) {
    						ta.append(line+"\r\n");
    					}
    					bufr.close();
    				}catch(IOException e1) {
    					throw new RuntimeException("读取失败");
    				}
    			}
    		});
    		
    		closeItem.addActionListener(new ActionListener() {     //菜单关闭事件
    
    			public void actionPerformed(ActionEvent arg0) {
    				System.exit(0);
    			}
    			
    		});
    		//关闭f窗体
    		f.addWindowListener(new WindowAdapter() {
    
    			public void windowClosing(WindowEvent arg0) {
    				
    				System.exit(0);
    			}
    		});
    	}
    	
    	public static void main(String[] args) {
    		new MyMenuDemo();
    	}
    
    }
## 11.保存文件
    package GUITest;
    
    import java.awt.*；
    import java.awt.event.*;
    import java.io.*;
    
    public class MyMenuDemo {
    	private Frame f;
    	private TextArea ta;
    	private MenuBar bar;
    	private Menu fileMenu;
    	private MenuItem openItem,saveItem,closeItem;
    	private File file;
    	
    	private FileDialog openDia,saveDia;
    	
    	MyMenuDemo(){
    		init();
    	}
    	
    	public void init() {
    		f=new Frame("记事本");
    		f.setBounds(300, 100, 650, 500);
    		
    		bar=new MenuBar();
    		ta=new TextArea();
    
    		fileMenu=new Menu("文件");
    		
    		openItem=new MenuItem("打开");
    		saveItem=new MenuItem("保存");
    		closeItem=new MenuItem("退出");
    		
    		fileMenu.add(openItem);
    		fileMenu.add(saveItem);
    		fileMenu.add(closeItem);
    
    		bar.add(fileMenu);
    		
    		f.setMenuBar(bar);
    		
    		
    		openDia=new FileDialog(f,"打开",FileDialog.LOAD);//打开
    		saveDia=new FileDialog(f,"保存",FileDialog.SAVE);//打开
    		
    		
    		f.add(ta);
    		MyEvent();
    		f.setVisible(true);
    	}
    	
    	private void MyEvent() {
    		saveItem.addActionListener(new ActionListener() {
    			public void actionPerformed(ActionEvent arg0) {
    				
    				if(file==null) {
    					saveDia.setVisible(true);
    					String dirPath=saveDia.getDirectory();
    					String fileName=saveDia.getFile();
    					if(dirPath==null||fileName==null)
    						return;
    					file=new File(dirPath,fileName);
    				
    				}
    				try {
    					BufferedWriter bufw=new BufferedWriter(new FileWriter(file));
    					
    					String  text=ta.getText();
    					
    					bufw.write(text);
    					bufw.flush();
    					bufw.close();
    					
    				}catch(IOException e2) {
    					throw new RuntimeException();
    				}
    			}
    		});
    		
    		
    		openItem.addActionListener(new ActionListener() {
    			
    		
    			public void actionPerformed(ActionEvent e) {
    				openDia.setVisible(true);
    				String dirPath=openDia.getDirectory();
    				String fileName=openDia.getFile();
    				System.out.println(dirPath+"......"+fileName);
    				if(dirPath==null||fileName==null)
    					return;
    				ta.setText("");
    				file=new File(dirPath,fileName);
    				try {
    					BufferedReader bufr=new BufferedReader(new FileReader(file));
    					String line=null;
    					
    					while((line=bufr.readLine())!=null) {
    						ta.append(line+"\r\n");
    					}
    					bufr.close();
    				}catch(IOException e1) {
    					throw new RuntimeException("读取失败");
    				}
    			}
    		});
    		
    		closeItem.addActionListener(new ActionListener() {     //菜单关闭事件
    			public void actionPerformed(ActionEvent arg0) {
    				
    				System.exit(0);
    			}
    			
    		});
    		//关闭f窗体
    		f.addWindowListener(new WindowAdapter() {
    
    			public void windowClosing(WindowEvent arg0) {
    			
    				System.exit(0);
    			}
    		});
    	}
    	
    	public static void main(String[] args) {
    		new MyMenuDemo();
    	}
    
    }
