package exec;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class ExecTest {
    public static void main(String[] args) {

        boolean flag=isOpenExec("notepad++.exe");
        System.out.println(flag);
        if(!flag){
            openExe();
        }

    }
    public static void openExe() {
        final Runtime runtime = Runtime.getRuntime();
        Process process = null;

        try {
            process = runtime.exec("C:\\Program Files\\Notepad++\\notepad++.exe");
            System.out.println("open");

        } catch (final Exception e) {
            System.out.println("Error exec!");
        }
    }
    public static List Tasklist()
    {
        List list=new ArrayList();
        try
        {
            Process process = Runtime.getRuntime().exec("tasklist");
            Scanner in=new Scanner(process.getInputStream());
            while(in.hasNextLine()){
                String p=in.nextLine();
                System.out.println(p);
                list.add(p);
            }
        }
        catch(Exception ex)
        {
            ex.printStackTrace();
        }
        return list;
    }

    public static boolean isOpenExec(String taskName){
        Process process=null;
        try
        {
            process = Runtime.getRuntime().exec("tasklist");

        }
        catch(Exception ex)
        {
            ex.printStackTrace();
        }

        Scanner in=new Scanner(process.getInputStream());
        while(in.hasNextLine()){
            String p=in.nextLine();
            String curtaskName=p.split(" ")[0];
            if(taskName.equals(curtaskName)){
                System.out.println(curtaskName);
                return true;
            }
        }

        return false;
    }


}
