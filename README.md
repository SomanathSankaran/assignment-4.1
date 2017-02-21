# assignment-4.1
QN 1Write a Java program, to take a HDFS Path as input and display all the files and sub-directories
in that HDFS path.

import java.io.*;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.fs.FileStatus;

public class FileListing {
	public static void main(String[] args) {
		if (args.length != 1) {
			System.out.println("Pass one argument");
			System.exit(1);
		}
		
		Path path = new Path(args[0]);
		
		try
		{
			Configuration conf = new Configuration();
			FileSystem fs = FileSystem.get(path.toUri(), conf);
			FileStatus[] fst=fileSystem.listStatus(path);
			
			for (FileStatus m : fst) {
				if (m.isDirectory()) {
					System.out.println("Directory is " + fStat.getPath());
				}
				else if (m.isFile()) {
					System.out.println("File is" + fStat.getPath());
				}
				else if (m.isSymlink()) {
					System.out.println("Symlink is" + fStat.getPath());
				}
			}

		}
		catch (IOException e)
		{
            e.printStackTrace();
		}
	}
}


QN 2Modify the previous program to list all the files and sub-directories in the HDFS path
recursively.

import java.io.*;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.fs.FileStatus;

public class FileListing {
	public static void main(String[] args) {
		if (args.length != 1) {
			System.out.println("Pass one argument");
			System.exit(1);
		}
		
		Path path = new Path(args[0]);
		
		try
		{
			Configuration conf = new Configuration();
			FileSystem fs = FileSystem.get(path.toUri(), conf);
			RemoteIterator<LocatedFileStatus> rit=fs.listFiles(path,true);//true for recursive operation
      while(rit.hasNext())
      {
      System.out.println(rit.next().getpath());
			}

		}
		catch (IOException e)
		{
            e.printStackTrace();
		}
	}
}
QN 3 Modify the previous program to take multiple HDFS paths (separated by space) and list all the
files and sub-directories in those HDFS paths recursively.
Since terminal will automatically take the arguement as seperated and when I gave two directories   /temp/user
all directories and sub directories will be listed 
import java.io.*;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.fs.FileStatus;

public class FileListing {
	public static void main(String[] args) {
		int k=args.length//k has the total number of arguments
		Path[] path = new Path[k];
		for(int f=0;f<k;f++)
		try
		{
		path[f]=path[args[f]];
			Configuration conf = new Configuration();
			FileSystem fs = FileSystem.get(path[f].toUri(), conf);
			RemoteIterator<LocatedFileStatus> rit=fs.listFiles(path[f],true);//true for recursive operation
      while(rit.hasNext())
      {
      System.out.println(rit.next().getpath());
			}

		}
		catch (IOException e)
		{
            e.printStackTrace();
		}
	}
}
