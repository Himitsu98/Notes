###多类合作

```java
/*
电脑: 可以看做是一个类
    成员变量: 品牌 颜色 系统名
    成员方法: 敲代码
电脑专修学院:
    成员变量: 地址，电话，联系人
    成员方法: 装系统
        【重点】装系统的方法，需要一个电脑，需要一个电脑类的对象
*/

/*
电脑类:
    成员变量：
        屏幕类对象
        键盘类对象
    成员方法：
        换屏幕
        换键盘

屏幕类:
    成员变量:
        品牌
键盘类:
    成员变量：
        品牌
*/

class PC {
    String name;
    String color;
    String systemName;

    public PC() {}
    public PC(String name, String color, String systemName) {
        this.name = name;
        this.color = color;
        this.systemName = systemName;        
    }

    public void  coding() {
        if (systemName != null) {
            System.out.println("键盘敲烂，月薪过万，键盘落灰，狗屎一堆");
        } else {
            System.out.println("系统崩溃");
        }        
    }
}
class RPC {
    String address;
    String telephone;
    String person;

    public RPC() {}
    public RPC(String address, String telephone, String person) {
        this.address = address;
        this.telephone = telephone;
        this.person = person;
    }
    /*
    需要一台电脑，来进行修理
    需要把PC类对象作为当前方法的参数，传入到RPC的方法中
    */

    /**
    *修理电脑的方法，需要的参数是PC类的一个类对象
    *@param p PC类的一个类对象，需要修理的电脑
    */
    public void repair(PC p) throws InterruptedException {
        //如果电脑为null，表示需要装系统
        //如果不为null，则报错
        if (null == p.systemName) {
            for (int i = 0; i < 10; i++) {
                System.out.println("Loading......." + (i  * 10) + "%");
                Thread.sleep(1000);
            }
        } else {
            System.out.println("Error Input");
        }
        p.systemName = "Windows 10";
        System.out.println("Install Complete");    
    }
}

public class Demo {
    public static void main(String[] args) throws InterruptedException {
        PC pc = new PC("ACER", "Black", "Windows 10");

        for (int i = 0; i < 10; i++) {
            pc.coding();
            Thread.sleep(500);
        }

        //系统炸了
        pc.systemName = null;
        pc.coding();

        RPC rpc = new RPC("唐宁街10号", "12345678", "Jack");
        rpc.repair(pc);

        for (int i = 0; i < 10; i++) {
            pc.coding();
            Thread.sleep(500);
        }

    }
}

//---------------------------------------------------

class KeyBoard {
    private String KBname;

    public KeyBoard() {}

    public KeyBoard(String name) {
        this.KBname = name;
    }

    public void setKBName(String name) {
        this.KBname = name;
    }

    public String getKBName() {
        return KBname;
    }
}

class Screen {
    private String SName;
    public Screen() {}
    public Screen(String name) {
        this.SName = name;
    }

    public void setSName(String name) {
        this.SName = name;
    }

    public String getSName() {
        return SName;
    }
}

class Computer {
    private Screen screen;
    private KeyBoard keyboard;

    public Computer() {}
    public Computer(Screen s, KeyBoard k) {
        this.screen = s;
        this.keyboard = k;
    }

    public void setScreen(Screen s) {
        this.screen = s;
    }
    public Screen getScreen() {
        return screen;
    }
    public void setKeyBoard(KeyBoard keyBoard) {
        this.keyboard = keyBoard;
    }
    public KeyBoard getKeyBoard() {
        return this.keyboard;
    }

    public void show() {
        System.out.println("Screen : " + screen.getSName()
                + " KeyBoard : " + keyboard.getKBName());
    }
}

public class Demo {
    public static void main(String[] args) {
        KeyBoard kb = new KeyBoard();
        kb.setKBName("Filco");

        Screen s = new Screen();
        s.setSName("DELL");

        Computer c = new Computer(s,kb);

        c.show();

        System.out.println("Screen boomed");

        c.setScreen(new Screen("LG"));
        c.show();

        System.out.println("keyBoard boomed");
        KeyBoard  nkb = new KeyBoard("Cherry");
        c.setKeyBoard(nkb);
        c.show();
    }
}
```
**提醒**：
　　1.当需要将一行代码进行折叠以便阅读时，尽量将 + 号放到第二行开头，提醒这一行与上一行相连
　　2.Java要求main函数所在类，必须是public修饰的公共类，以便于外部程序对主方法的访问
