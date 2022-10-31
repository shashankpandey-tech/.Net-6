# .Net-6
# Whats new in .Net 6 linq new suff?
# .Net 6 Official - https://learn.microsoft.com/en-us/dotnet/core/whats-new/dotnet-6

# Below are new LINQ features:

1. New methods MaxBy and MinBy
2. New methods Chunk
3. New methods DistinctBy, UnionBy, IntersectBy, and ExceptBy
4. Index and Range parameters
5. New method TryGetNonEnumeratedCount
6. Default parameters for FirstOrDefault, LastOrDefault, and SingleOrDefault
7. Zip supports 3 IEnumerables

# Examples 

# 1. MaxBy and MinBy

var employee = new List<Employee>
{
    new Employee { Id = 1, Name = "Shashank", Age = 38},
    new Employee { Id = 2, Name = "Ram", Age = 36},
    new Employee { Id = 3, Name = "Sohan", Age = 34},
    new Employee { Id = 4, Name = "Raman", Age = 29},
};
  
//Without using MaxBy and MinBy
var oldestEmployee = employee.OrderByDescending(emp => emp.Age).First();
var youngestEmployee = employee.OrderBy(emp => emp.Age).First();

var oldestEmployee = employee.MaxBy(emp => emp.Age);
var youngestEmployee = employee.MinBy(emp => emp.Age);

# Chunk Methos -

IEnumerable<Employee[]> cluster = employee.Chunk(2);
// Print each cluster.
foreach(var employee in cluster)
{
    Console.WriteLine($"Cluster of {string.Join(",", employee.Select(emp => emp.Name))}");
}
//Prints
// Cluster of Shashank,Ram
// Cluster of Sohan,Raman

New methods DistinctBy, UnionBy, IntersectBy, and ExceptBy -

var evenAgedEmployee = employee.Where(emp => emp.Age % 2 == 0); //Shashank,Ram,Sohan

var employeeAbove35 = employee.Where(emp => emp.Age > 35); //Shashank,Ram

var union = evenAgedEmployee.UnionBy(employeeAbove35, x => x.Age); //Shashank,Ram,Sohan

var intersection = evenAgedEmployee.IntersectBy(employeeAbove35.Select(p => p.Age), x => x.Age); //Shashank,Ram

The ElementAt operator now takes indices from the end. -

var secondLastEmployee = employee.ElementAt(^2); // "Sohan"

Skip and Take now take Range as well:

var take3Employee = employee.Take(..3); //Shashank,Ram,Sohan

var skip1Employee =  employee.Take(1..); //Ram,Sohan,Raman

var take3Skip1Employee = employee.Take(1..3); //Ram,Sohan

var takeLast2Employee = employee.Take(^2..); //Sohan,Raman

var skipLast3Employee = employee.Take(..^3); //Shashank

var takeLast3SkipLast2 = employee.Take(^3..^2); //Ram
