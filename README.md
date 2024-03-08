# POS_Test

## ViewBag

```c#
public IActionResult CreateSpeiseForm()
{
    //// Informationen für eine Drop-Down-Liste bereitstellen
    List<SelectListItem> selectListItems = new List<SelectListItem>();
    SelectListItem eintrag1 = new SelectListItem("Yummy Good", "5");
    selectListItems.Add(eintrag1);
    SelectListItem eintrag2 = new SelectListItem("Good", "4");
    selectListItems.Add(eintrag2);
    SelectListItem eintrag3 = new SelectListItem("Nice", "3");
    selectListItems.Add(eintrag3);
    SelectListItem eintrag4 = new SelectListItem("Ok", "2");
    selectListItems.Add(eintrag4);
    SelectListItem eintrag5 = new SelectListItem("Awful", "1");
    selectListItems.Add(eintrag5);
    
    // Die Übergabe erfolgt über das ViewData-Dictionary
    ViewData["Kategorien"] = selectListItems;

    return View();
}
```
Erstellen von einer ViewData mit Namen "Kategorie"

```c#
<select asp-for="Sterne" form-control" asp-items="@((IEnumerable<SelectListItem>)ViewData["Kategorien"])"></select>
```
In CreateSpeiseForm wird diese dann abgerufen

## Datenbank

1. Nugets installieren
Core.Design
Core.Sqlite
Core.Tools

2. Application DB Context
```c#
public class ApplicationDbContext : DbContext
{
    // DBSet
    public DbSet<Speise> Speisen { get; set; }
    public DbSet<Zutat> Zutaten { get; set; }

    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options)
    {

    }
}
```
Hier werden die Models Speise und Zutat erstellt

3. Program.cs
```c#
            var connectionString = builder.Configuration.GetConnectionString("SpeisenDb");
            builder.Services.AddDbContext<ApplicationDbContext>(options => options.UseSqlite(connectionString));
```
In der Program.cs den ConnectionString festlegen 

4. Connected Services
Neuen Service SQLite-Datenbank

5. Datenbank aufsetzen
Wie immer add-migration und update-database
