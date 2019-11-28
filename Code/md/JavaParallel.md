#  Java 线程和 特别的JavaFx线程

多线程输出100个a，100个b，1~100

OutPut.java

```java
public class OutPut {

    public static void main(String[] args) {
        Runnable a1=new print1();
        Runnable a2=new print2();
        Runnable a3=new print3();
        Thread t1=new Thread(a1);
        Thread t2=new Thread(a2);
        Thread t3=new Thread(a3);
        t1.start();//三线程一一启动，开始并行，屏幕打印权在他们之前传来传去
        t2.start();
        t3.start();
    }
}
class print1 implements Runnable{
    public void run(){
        for(int i = 1;i<=100;i++)
        System.out.print(i+ " ");
    }
}
class print2 implements Runnable{
    public void run(){
        for(int i = 1;i<=100;i++)
            System.out.print("a"+" ");
    }
}
class print3 implements Runnable{
    public void run(){
        for(int i = 1;i<=100;i++)
            System.out.print("b"+" ");
    }
}
```

效果（5次）

![1](photo/JavaParallel1.png)

![1](photo/JavaParallel2.png)

![1](photo/JavaParallel3.png)

![1](photo/JavaParallel4.png)

![1](photo/JavaParallel5.png)

可见，每次输出不完全相同。

# JavaFx闪烁框：



```java

import javafx.application.Application;
import javafx.application.Platform;
import javafx.fxml.FXMLLoader;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.layout.StackPane;
import javafx.stage.Stage;

public class Main extends Application {
    private String text="";//初始化要显示的值text
    @Override
    public void start(Stage primaryStage) throws Exception{
        StackPane pane = new StackPane();//创建画布
        Label lblText = new Label();//java标签组件 JLabel
        pane.getChildren().add(lblText);
        new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    while(true){
                        if(lblText.getText().trim().length()==0)
                            text="Welcome to Dragon WorkSpace";
                        else
                            text="";
                        Platform.runLater(new Runnable() {
                            @Override
                            public void run() {
                                lblText.setText(text);//lblText要在Platform下才能使用线程控制其闪烁，普通的thread只能控制一般的文本框状态。还可以使用第二种方法TimeLine通过帧来控制
                            }
                        });
                        Thread.sleep(200);
                    }
                }
                catch (InterruptedException ex){
                }
            }
        }).start();
        Scene scene = new Scene(pane,200,50);//创建屏幕
        primaryStage.setTitle("Flash Text");
        primaryStage.setScene(scene);
        primaryStage.show();//主线程运行与副线程们并不冲突。在primaryStage使用show方法之前，lblText并不会实际显示，只是不断setText更改里面的字符。
    }


    public static void main(String[] args) {
        launch(args);
    }
}
```

### 实际效果



![6](photo/JavaParallel6.PNG)

![7](photo/JavaParallel7.png)

![6](photo/JavaParallel6.PNG)

![7](photo/JavaParallel7.png)

#### 两张照片不断闪烁

> 以上仅是个人看法，如有错误，敬请指正。 工作邮箱：Dragonroot2018@gmail.com