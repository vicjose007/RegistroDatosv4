```c#
using System;

using System.IO;

using System.Collections.Generic;

using System.Threading.Tasks;

using System.Text;

namespace registro

{

class Program

{

static void Main(string[] args)

{

Console.WriteLine("Ingrese su Password");

string Password = Console.ReadLine();

Console.WriteLine("Confirme su Password");

string confirmPassword = Console.ReadLine();

while(Password != confirmPassword)

{

Console.Clear();

Console.WriteLine("Password Equivocado");

Console.WriteLine("Confirme su Password");

confirmPassword = Console.ReadLine();

}

Console.WriteLine("Seleccione la opcion que desee\n"

+ "1) Registrar\n" + "2) Buscar a travez de la Cedula \n" + "3) Lista \n" + "4) Eliminar archivo\n");

int Select = int.Parse(Console.ReadLine());

switch(Select)

{

case 1:

Console.Clear();

Console.WriteLine("Ingrese su nombre");

string name = Console.ReadLine();

if(typeCheckInt(name)== true)

{

Console.WriteLine("No ingrese numeros");

return;

}

else

{

Console.WriteLine("Bienvenido " + name);

}

Console.WriteLine("Ingrese su apellido");

string lastname = Console.ReadLine();

if(typeCheckInt(lastname)== true)

{

Console.WriteLine("No ingrese numeros");

return;

}

else

{

Console.WriteLine(name + " " + lastname);

}

try

{

Console.WriteLine("Ingrese su edad");

int age = int.Parse(Console.ReadLine());

Console.WriteLine("Ingrese su cedula");

int cedula = int.Parse(Console.ReadLine());

try

{

using(Stream datos = new FileStream("C:/Users/vicjo/OneDrive/Desktop/data/regdatos.csv",FileMode.Append,FileAccess.Write))

{

using(StreamWriter output = new StreamWriter(datos))

{

output.WriteLine(name + ',' + lastname + ',' + age + ',' + cedula +',');

}

}

}

catch(Exception ex)

{

Console.WriteLine(ex.Message);

}

}

catch(Exception error)

{

Console.WriteLine("No ingrese letras, solo numeros" + error.Message);

}

break;

case 2:

{

FileStream insideFile = new FileStream("C:/Users/vicjo/OneDrive/Desktop/data/regdatos.csv", FileMode.Open, FileAccess.Read);

StreamReader reader = new StreamReader(insideFile);

string save;

string cedula;

Console.WriteLine("Ingrese la cedula porfavor:");

cedula = Console.ReadLine();

try

{

save = reader.ReadLine();

while(save != null)

{

if(save.Contains(cedula))

{

Console.WriteLine(save);

}

save = reader. ReadLine();

}

}

finally

{

reader.Close();

insideFile.Close();

}

}

break;

case 3:

Console.Clear();

Stream lst = new FileStream("C:/Users/vicjo/OneDrive/Desktop/data/regdatos.csv", FileMode.Open, FileAccess.Read);

StreamReader file = new StreamReader(lst);

while(!file.EndOfStream)

{

Console.WriteLine(file.ReadLine());

}

break;

case 4:

Console.Clear();

try

{

File.Delete("C:/Users/vicjo/OneDrive/Desktop/data/regdatos.csv");

Console.WriteLine("El archivo a sido borrado");

}

catch(Exception ex)

{

Console.WriteLine(ex.ToString());

}

break;

}

static bool typeCheckInt(String input)

{

int number = 0;

return int.TryParse(input,out number);

}

}

}

}
```