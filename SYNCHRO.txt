import java.util.*; 
import java.util.concurrent.Semaphore; 

//above classes aint' used, as signal and wait methods are defined explicitly.on line 32 and 39.
public class synchronizationClassicalProb { 
    static int mutex=1; 
    static int database=1; 
    static int Read_Count=0; 
    static void Reader() throws Exception 
    { 
        while(true) 
        { 
            mutex=wait(mutex); 
            Read_Count=Read_Count+1; 
            if(Read_Count==1){ 
                database=signal(database); 
            } 
            mutex=signal(mutex); 
            System.out.println(Read_Count+ " User Reading the Data........."); 
            mutex=wait(mutex); 
            Read_Count=Read_Count-1; 
            if(Read_Count==0) 
            { 
                database=signal(database); 
            } 
            mutex=signal(mutex); 
            System.out.println("Reading Finished!!!!!!"); 
            break; 
            
        } 
    } 
    static int wait(int mutex)
    { 
        while(mutex<=0) 
            break ; 
        mutex=mutex-1; 
        return mutex; 
    } 
    static int signal(int database) 
    { 
        database=database+1; 
        return database; 
    } 
    static void Writer() throws Exception 
    { 
        while(true) 
        { 
            database=wait(database); 
            System.out.println("Writing on the database......"); 
            database=signal(database); 
            System.out.println("Writing Finished!!!!!."); 
            break; 
        } 
    } 
    public static void main(String[] args)throws Exception { 
        Writer(); 
        Reader(); 
        Reader(); 
         
    } 
}