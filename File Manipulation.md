# File Manipulation / System.IO

## Why This Topic Matters ?
this topic make us know about file in .net
and how add file or write or read

## file
we have two type of file 
Binary files (store data in the same format that computer has in main memory)
Text files (sotre data in numeric values have been converted into string of ASCII characters) 
### class in System-IO
| class   |      Description      |
|----------|:-------------:|
| FileStream |  acess to input and output | 
| StreamReader |    read a stream   |  
| StreamWrite | write a stream |
| File | some opertaion on the file |

## File
Method 

- WriteAllText
- WriteAllLines
- ReadAllText
- ReadAllLines
- AppendAllText
- AppendAllLines
note:

(if method have Text => string)

(if method have Lines => string[])

(have there start words: Write,Read,Append)
### Create File
```cs
 if (File.Exists(pathName))
            {
                Console.WriteLine("File is Exists.");
            }
            else
            {
                Console.WriteLine("File is not Exists.");
            }
```
###  WriteAllText
```cs

static void WriteAllText(string filePath, string text) 
        { 
            File.WriteAllText(filePath, text);
        }
```
### ReadAllText
```cs

static void FileReadAllText(string pathName) 
        {
            Console.WriteLine(File.ReadAllText(pathName));
        }
```
### ReadAllLines
```cs

 static void FileReadAllLines(string pathName)
        {
            string[] file = File.ReadAllLines(pathName);
            foreach (string line in file)
            {
                Console.WriteLine(line);
            }
        }
```
### Append
```cs

 static void FileAppendText(string pathName, string[] texts,string text) 
        {
            File.AppendAllText(pathName, text);
            File.AppendAllLines(pathName, texts);
        }
```

## CSV
Within the File Class, you are not restricted to just text files, it is possible to expand it out to.csv files as well.The most important part about.csv files is to note that each piece of data is separated by a comma.You must also note line endings by noting a '\n'. This indicates to start the next column of the.csv.
A CSV(comma-separated values) file is a text file in which information is separated by commas.
CSV files are most commonly encountered in spreadsheets and databases.
You can use a CSV file to move data between programs that aren't ordinarily able to exchange data.

```cs

static void FileCsv()
        {
            string path = @"F:\asac\New folder\file.csv";
            string[] catInformation = { "Name,7", "Belle,6", "Josie,6" };

           

            File.WriteAllLines(path, catInformation);

            string[] catNames = File.ReadAllLines(path);

            for (int i = 0; i < catNames.Length; i++)
            {
                string[] fields = catNames[i].Split(',');
                string name = fields[0];
                int age = Convert.ToInt32(fields[1]);
                Console.WriteLine($"Name: {name} Age: {age}");
            }

        }
```

## Stream 

- more control over your reading and writing
- working with individual bytes
- can work directly with strings, ints, and other types within the write method

### StreamWrite
```cs

  static void StreamToWrite(string pathName) 
        {
        FileStream fs = File.OpenWrite(pathName);
        StreamWriter writer = new StreamWriter(fs);
            writer.WriteLine(5);
            writer.WriteLine("text to add");
            writer.Close();

        }
```

### Append
```cs

 static void FileAppendText(string pathName, string[] texts,string text) 
        {
            File.AppendAllText(pathName, text);
            File.AppendAllLines(pathName, texts);
        }
```

### Append
```cs

 static void FileAppendText(string pathName, string[] texts,string text) 
        {
            File.AppendAllText(pathName, text);
            File.AppendAllLines(pathName, texts);
        }
```
## Things I want to know more about

- stream with binary 
