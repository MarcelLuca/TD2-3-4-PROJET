# DemoApi — Guide complet : créer une API ASP.NET Core avec C# (SQL Server + EF Core + Swagger)
**Projet : DemoApi — Guide pour débutants (avec PROJET FINAL + BONUS)**

Ce READ vous accompagne étape par étape pour créer votre première API web avec **ASP.NET Core**, **SQL Server (LocalDB)** et **Entity Framework Core**, avec une interface web simple en **HTML/JavaScript** et une documentation **Swagger/OpenAPI obligatoire**.

---

## ✅ Table des matières
- [PARTIE 1 : PRÉPARATION DE L'ENVIRONNEMENT](#partie-1--préparation-de-lenvironnement)
  - [ÉTAPE 1.1 : Installer Visual Studio](#étape-11--installer-visual-studio)
  - [ÉTAPE 1.2 : Vérifier l'installation](#étape-12--vérifier-linstallation)
- [PARTIE 2 : CRÉER LE PROJET](#partie-2--créer-le-projet)
  - [ÉTAPE 2.1 : Créer un nouveau projet](#étape-21--créer-un-nouveau-projet)
  - [ÉTAPE 2.2 : Configurer le projet](#étape-22--configurer-le-projet)
- [PARTIE 3 : COMPRENDRE LA STRUCTURE DU PROJET](#partie-3--comprendre-la-structure-du-projet)
- [PARTIE 4 : CONFIGURER LA BASE DE DONNÉES](#partie-4--configurer-la-base-de-données)
  - [ÉTAPE 4.1 : Installer les packages NuGet nécessaires](#étape-41--installer-les-packages-nuget-nécessaires)
  - [ÉTAPE 4.2 : Configurer la chaîne de connexion](#étape-42--configurer-la-chaîne-de-connexion)
- [PARTIE 5 : CRÉER LE MODÈLE (MODEL)](#partie-5--créer-le-modèle-model)
  - [ÉTAPE 5.1 : Créer la classe Product](#étape-51--créer-la-classe-product)
  - [ÉTAPE 5.2 : Comprendre les propriétés C#](#étape-52--comprendre-les-propriétés-c)
- [PARTIE 6 : CRÉER LE CONTEXTE DE BASE DE DONNÉES](#partie-6--créer-le-contexte-de-base-de-données)
  - [ÉTAPE 6.1 : Créer AppDbContext](#étape-61--créer-appdbcontext)
- [PARTIE 7 : CRÉER LE SERVICE (COUCHE MÉTIER)](#partie-7--créer-le-service-couche-métier)
  - [ÉTAPE 7.1 : Créer l'interface IProductService](#étape-71--créer-linterface-iproductservice)
  - [ÉTAPE 7.2 : Créer ProductService (implémentation)](#étape-72--créer-productservice-implémentation)
- [PARTIE 8 : CRÉER LE CONTRÔLEUR (API ENDPOINTS)](#partie-8--créer-le-contrôleur-api-endpoints)
  - [ÉTAPE 8.1 : Créer ProductsController](#étape-81--créer-productscontroller)
- [PARTIE 9 : CONFIGURER PROGRAM.CS](#partie-9--configurer-programcs)
  - [ÉTAPE 9.1 : Configurer les services dans Program.cs](#étape-91--configurer-les-services-dans-programcs)
- [PARTIE 10 : CRÉER LES MIGRATIONS ET LA BASE DE DONNÉES](#partie-10--créer-les-migrations-et-la-base-de-données)
  - [ÉTAPE 10.1 : Ouvrir la Console du Gestionnaire de Package](#étape-101--ouvrir-la-console-du-gestionnaire-de-package)
  - [ÉTAPE 10.2 : Créer la migration](#étape-102--créer-la-migration)
  - [ÉTAPE 10.3 : Appliquer la migration](#étape-103--appliquer-la-migration)
- [PARTIE 11 : CRÉER L'INTERFACE WEB (FRONTEND) + SWAGGER OBLIGATOIRE](#partie-11--créer-linterface-web-frontend--swagger-obligatoire)
  - [ÉTAPE 11.1 : Créer le dossier wwwroot](#étape-111--créer-le-dossier-wwwroot)
  - [ÉTAPE 11.2 : Créer index.html](#étape-112--créer-indexhtml)
  - [ÉTAPE 11.3 : Créer swagger.html (documentation API)](#étape-113--créer-swaggerhtml-documentation-api)
- [PARTIE 12 : LANCER ET TESTER L'APPLICATION](#partie-12--lancer-et-tester-lapplication)
- [PARTIE 13 : DÉBOGUAGE (RÉSOLUTION DE PROBLÈMES)](#partie-13--déboguage-résolution-de-problèmes)
- [PARTIE 14 : CONCEPTS CLÉS À RETENIR](#partie-14--concepts-clés-à-retenir)
- [PARTIE 15 : PROJET FINAL (BACKEND + FRONTEND + BONUS)](#partie-15--projet-final-backend--frontend--bonus)
  - [15.1 : API Fournisseurs](#151--api-fournisseurs-supplier)
  - [15.2 : API Matières Premières](#152--api-matières-premières-rawmaterial)
  - [15.3 : BONUS — Relations + recherche](#153--bonus--relations--recherche-de-produits)
- [RESSOURCES POUR ALLER PLUS LOIN](#ressources-pour-aller-plus-loin)
- [CONCLUSION](#conclusion)

---

# PARTIE 1 : PRÉPARATION DE L'ENVIRONNEMENT

## ÉTAPE 1.1 : Installer Visual Studio
1. Téléchargez **Visual Studio 2022 Community** (gratuit) depuis :  
   https://visualstudio.microsoft.com/downloads/

2. Lors de l'installation, sélectionnez la charge de travail :  
   ✅ **Développement web et ASP.NET**

   Cette charge de travail inclut :
   - .NET SDK
   - ASP.NET Core
   - Entity Framework Core
   - SQL Server Express LocalDB

3. Installez aussi **SQL Server Express** ou **LocalDB** (généralement inclus avec VS)

## ÉTAPE 1.2 : Vérifier l'installation
1. Ouvrez Visual Studio
2. Allez dans : **Aide > À propos de Microsoft Visual Studio**
3. Vérifiez que **.NET SDK 10.0** est installé

---

# PARTIE 2 : CRÉER LE PROJET

## ÉTAPE 2.1 : Créer un nouveau projet
1. Dans Visual Studio : **Fichier > Nouveau > Projet**
2. Recherchez : **ASP.NET Core Web API**
3. Sélectionnez le modèle **ASP.NET Core Web API**
4. Cliquez sur **Suivant**

## ÉTAPE 2.2 : Configurer le projet
1. Nom du projet : **DemoApi** (ou le nom de votre choix)
2. Emplacement : choisissez où sauvegarder votre projet
3. Solution : laissez **Créer une nouvelle solution**
4. Framework : sélectionnez **.NET 10.0** (ou .NET 8.0 si disponible)
5. Cochez :
   - ✅ Utiliser des contrôleurs
   - ✅ Activer OpenAPI (Swagger) (**OBLIGATOIRE**)
6. Cliquez sur **Créer**

### EXPLICATION : Qu'est-ce qu'un projet Web API ?
Une **Web API** est une application qui expose des endpoints (points d'accès) sur Internet.  
Ces endpoints permettent à d'autres applications (ou sites web) de récupérer ou envoyer des données via HTTP.

**Exemple :**
- `GET /api/products` retourne la liste des produits

---

# PARTIE 3 : COMPRENDRE LA STRUCTURE DU PROJET

Après la création, vous verrez ces dossiers :

- 📁 **Controllers/**
  - Contient les contrôleurs (les routes de votre API)
- 📁 **Models/**
  - Contient les modèles de données (classes qui représentent vos données)
- 📁 **Data/**
  - Contiendra le contexte de base de données (connexion à la DB)
- 📁 **Services/**
  - Contiendra la logique métier (règles de votre application)
- 📁 **wwwroot/**
  - Contient les fichiers statiques (HTML, CSS, images)
- 📄 **Program.cs**
  - Point d'entrée de l'application (configuration)
- 📄 **appsettings.json**
  - Fichier de configuration (chaînes de connexion, etc.)

---

# PARTIE 4 : CONFIGURER LA BASE DE DONNÉES

## ÉTAPE 4.1 : Installer les packages NuGet nécessaires
Les packages sont des bibliothèques de code pré-écrites qu'on utilise.

1. Clic droit sur le projet dans l'Explorateur de solutions
2. Sélectionnez **Gérer les packages NuGet...**
3. Onglet **Parcourir**
4. Installez ces packages (un par un) :

- ✅ **Microsoft.EntityFrameworkCore**  
  Version : 10.0.0  
  Utilité : Framework pour accéder aux bases de données

- ✅ **Microsoft.EntityFrameworkCore.SqlServer**  
  Version : 10.0.0  
  Utilité : Support spécifique pour SQL Server

- ✅ **Microsoft.EntityFrameworkCore.Tools**  
  Version : 10.0.0  
  Utilité : Outils pour créer les migrations

- ✅ **Microsoft.AspNetCore.OpenApi**  
  Version : 10.0.2  
  Utilité : Support OpenAPI/Swagger (documentation de l'API)

### EXPLICATION : Qu'est-ce qu'Entity Framework Core ?
Entity Framework Core (EF Core) est un ORM (Object-Relational Mapping).  
Il permet de travailler avec une base de données en utilisant des objets C# au lieu d'écrire du SQL directement.

## ÉTAPE 4.2 : Configurer la chaîne de connexion
1. Ouvrez le fichier **appsettings.json**
2. Ajoutez la section **ConnectionStrings** :

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=DemoApiDb;Trusted_Connection=True;TrustServerCertificate=True;"
  },
  "Logging": {
    ...
  }
}
```

**⚠️ Note importante :** Le double backslash `\\` est nécessaire dans le JSON pour échapper le backslash.

### EXPLICATION : Qu'est-ce qu'une chaîne de connexion ?
Une chaîne de connexion indique à l'application comment se connecter à la base de données :

- `Server=(localdb)\mssqllocaldb` → Où se trouve SQL Server (LocalDB)
- `Database=DemoApiDb` → Nom de votre base de données
- `Trusted_Connection=True` → Utilise l'authentification Windows
- `TrustServerCertificate=True` → Accepte le certificat SSL local

LocalDB est une version légère de SQL Server, parfaite pour le développement.

---

# PARTIE 5 : CRÉER LE MODÈLE (MODEL)

## ÉTAPE 5.1 : Créer la classe Product
1. Clic droit sur le dossier **Models**
2. Ajouter > Classe
3. Nom : **Product.cs**
4. Cliquez sur **Ajouter**

Remplacez tout le contenu par :

```csharp
using System.ComponentModel.DataAnnotations;

namespace DemoApi.Models;

public class Product
{
    public int Id { get; set; }

    [Required(ErrorMessage = "Le nom du produit est requis")]
    [MinLength(1, ErrorMessage = "Le nom doit contenir au moins 1 caractère")]
    public string Name { get; set; } = string.Empty;

    [Range(0.01, 1000000, ErrorMessage = "Le prix doit être entre 0.01 et 1,000,000")]
    public decimal Price { get; set; }
}
```

### EXPLICATION : Qu'est-ce qu'un modèle ?
Un modèle (Model) est une classe C# qui représente une entité de votre application.

## ÉTAPE 5.2 : Comprendre les propriétés C#
```csharp
public int Id { get; set; }
```

Ceci est une propriété automatique :
- `int` : type entier
- `Id` : nom
- `get; set;` : lecture / écriture

Équivalent à :

```csharp
private int _id;
public int Id 
{ 
    get { return _id; } 
    set { _id = value; } 
}
```

---

# PARTIE 6 : CRÉER LE CONTEXTE DE BASE DE DONNÉES

## ÉTAPE 6.1 : Créer AppDbContext
📁 `Data/AppDbContext.cs`

```csharp
using Microsoft.EntityFrameworkCore;
using DemoApi.Models;

namespace DemoApi.Data;

public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options) : base(options)
    {
    }

    public DbSet<Product> Products { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<Product>()
            .Property(p => p.Price)
            .HasPrecision(18, 2);
    }
}
```

---

# PARTIE 7 : CRÉER LE SERVICE (COUCHE MÉTIER)

## ÉTAPE 7.1 : Créer l'interface IProductService
📁 `Services/IProductService.cs`

```csharp
using DemoApi.Models;

namespace DemoApi.Services;

public interface IProductService
{
    Task<IEnumerable<Product>> GetAllAsync();
    Task<Product?> GetByIdAsync(int id);
    Task<IEnumerable<Product>> GetMoreExpensiveThanAsync(decimal minPrice);
    Task<Product> CreateAsync(string name, decimal price);
    Task<bool> UpdatePriceAsync(int id, decimal newPrice);
}
```

## ÉTAPE 7.2 : Créer ProductService (implémentation)
📁 `Services/ProductService.cs`

```csharp
using Microsoft.EntityFrameworkCore;
using DemoApi.Data;
using DemoApi.Models;

namespace DemoApi.Services;

public class ProductService : IProductService
{
    private readonly AppDbContext _context;

    public ProductService(AppDbContext context)
    {
        _context = context;
    }

    public async Task<IEnumerable<Product>> GetAllAsync()
    {
        return await _context.Products
            .AsNoTracking()
            .ToListAsync();
    }

    public async Task<Product?> GetByIdAsync(int id)
    {
        return await _context.Products
            .AsNoTracking()
            .FirstOrDefaultAsync(p => p.Id == id);
    }

    public async Task<IEnumerable<Product>> GetMoreExpensiveThanAsync(decimal minPrice)
    {
        return await _context.Products
            .AsNoTracking()
            .Where(p => p.Price > minPrice)
            .OrderBy(p => p.Price)
            .ToListAsync();
    }

    public async Task<Product> CreateAsync(string name, decimal price)
    {
        var product = new Product
        {
            Name = name,
            Price = price
        };

        _context.Products.Add(product);
        await _context.SaveChangesAsync();
        return product;
    }

    public async Task<bool> UpdatePriceAsync(int id, decimal newPrice)
    {
        var product = await _context.Products.FindAsync(id);
        if (product == null)
        {
            return false;
        }

        product.Price = newPrice;
        await _context.SaveChangesAsync();
        return true;
    }
}
```

---

# PARTIE 8 : CRÉER LE CONTRÔLEUR (API ENDPOINTS)

## ÉTAPE 8.1 : Créer ProductsController
📁 `Controllers/ProductsController.cs`

```csharp
using System.ComponentModel.DataAnnotations;
using Microsoft.AspNetCore.Mvc;
using DemoApi.Services;

namespace DemoApi.Controllers;

[ApiController]
[Route("api/[controller]")]
public class ProductsController : ControllerBase
{
    private readonly IProductService _productService;

    public ProductsController(IProductService productService)
    {
        _productService = productService;
    }

    [HttpGet]
    public async Task<ActionResult<IEnumerable<object>>> GetAll()
    {
        var products = await _productService.GetAllAsync();
        return Ok(products);
    }

    [HttpGet("{id}")]
    public async Task<ActionResult<object>> GetById(int id)
    {
        var product = await _productService.GetByIdAsync(id);
        if (product == null)
        {
            return NotFound();
        }
        return Ok(product);
    }

    [HttpGet("expensive")]
    public async Task<ActionResult<IEnumerable<object>>> GetExpensive([FromQuery] decimal minPrice)
    {
        var products = await _productService.GetMoreExpensiveThanAsync(minPrice);
        return Ok(products);
    }

    [HttpPost]
    public async Task<ActionResult<object>> Create([FromBody] CreateProductRequest request)
    {
        if (!ModelState.IsValid)
        {
            return BadRequest(ModelState);
        }

        var product = await _productService.CreateAsync(request.Name, request.Price);
        return CreatedAtAction(nameof(GetById), new { id = product.Id }, product);
    }

    [HttpPut("{id}/price")]
    public async Task<IActionResult> UpdatePrice(int id, [FromQuery] decimal newPrice)
    {
        if (newPrice < 0.01m || newPrice > 1000000m)
        {
            return BadRequest("Le prix doit être entre 0.01 et 1,000,000");
        }

        var success = await _productService.UpdatePriceAsync(id, newPrice);
        if (!success)
        {
            return NotFound();
        }
        return NoContent();
    }

    public class CreateProductRequest
    {
        [Required(ErrorMessage = "Le nom du produit est requis")]
        [MinLength(1, ErrorMessage = "Le nom doit contenir au moins 1 caractère")]
        public string Name { get; set; } = string.Empty;

        [Required]
        [Range(0.01, 1000000, ErrorMessage = "Le prix doit être entre 0.01 et 1,000,000")]
        public decimal Price { get; set; }
    }
}
```

---

# PARTIE 9 : CONFIGURER PROGRAM.CS

## ÉTAPE 9.1 : Configurer les services dans Program.cs
📄 `Program.cs`

```csharp
using Microsoft.EntityFrameworkCore;
using DemoApi.Data;
using DemoApi.Services;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

var connectionString = builder.Configuration.GetConnectionString("DefaultConnection");
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(connectionString));

builder.Services.AddScoped<IProductService, ProductService>();

builder.Services.AddOpenApi();
builder.Services.AddEndpointsApiExplorer();

var app = builder.Build();

app.MapOpenApi();

app.UseHttpsRedirection();
app.UseStaticFiles();
app.UseAuthorization();
app.MapControllers();

app.Run();
```

---

# PARTIE 10 : CRÉER LES MIGRATIONS ET LA BASE DE DONNÉES

## ÉTAPE 10.1 : Ouvrir la Console du Gestionnaire de Package
Visual Studio :  
**Outils > Gestionnaire de packages NuGet > Console du Gestionnaire de packages**

## ÉTAPE 10.2 : Créer la migration
Dans la console :

```powershell
Add-Migration InitialCreate
```

## ÉTAPE 10.3 : Appliquer la migration
Toujours dans la console :

```powershell
Update-Database
```

---

# PARTIE 11 : CRÉER L'INTERFACE WEB (FRONTEND) + SWAGGER OBLIGATOIRE

✅ Swagger est obligatoire sur TOUT le projet (Products + Suppliers + RawMaterials + BONUS Search).

## ÉTAPE 11.1 : Créer le dossier wwwroot
Le dossier `wwwroot` devrait déjà exister, sinon :
- Clic droit sur le projet > Ajouter > Nouveau dossier
- Nom : `wwwroot`

## ÉTAPE 11.2 : Créer index.html
📁 `wwwroot/index.html`

**Objectif :**
- Ajouter des produits
- Visualiser la liste
- Filtrer les produits chers
- Mettre à jour le prix d'un produit

**Code complet à copier :**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DemoApi - Product Manager</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            padding: 30px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
        }

        h1 {
            color: #333;
            margin-bottom: 30px;
            text-align: center;
        }

        .form-section {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 30px;
        }

        .form-section h2 {
            color: #555;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .form-group {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            color: #333;
            font-weight: 500;
        }

        input {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 14px;
        }

        input:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        button {
            background: #667eea;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 14px;
            font-weight: 500;
            transition: background 0.3s;
        }

        button:hover {
            background: #5568d3;
        }

        button:disabled {
            background: #ccc;
            cursor: not-allowed;
        }

        .filter-section {
            background: #fff3cd;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 30px;
        }

        .filter-section h3 {
            color: #856404;
            margin-bottom: 10px;
        }

        .filter-controls {
            display: flex;
            gap: 10px;
            align-items: flex-end;
        }

        .filter-controls .form-group {
            flex: 1;
            margin-bottom: 0;
        }

        .products-section h2 {
            color: #555;
            margin-bottom: 15px;
        }

        .products-list {
            display: grid;
            gap: 15px;
        }

        .product-card {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 6px;
            border-left: 4px solid #667eea;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .product-info {
            flex: 1;
        }

        .product-name {
            font-weight: 600;
            color: #333;
            margin-bottom: 5px;
        }

        .product-price {
            color: #666;
            font-size: 0.9em;
        }

        .product-actions {
            display: flex;
            gap: 10px;
        }

        .btn-update {
            background: #28a745;
        }

        .btn-update:hover {
            background: #218838;
        }

        .message {
            padding: 10px;
            border-radius: 4px;
            margin-bottom: 15px;
            display: none;
        }

        .message.success {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .message.error {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .message.show {
            display: block;
        }

        .loading {
            text-align: center;
            padding: 20px;
            color: #666;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>📦 DemoApi - Product Manager</h1>

        <div id="message" class="message"></div>

        <div class="form-section">
            <h2>Add New Product</h2>
            <form id="productForm">
                <div class="form-group">
                    <label for="productName">Product Name:</label>
                    <input type="text" id="productName" name="name" required minlength="1" placeholder="Enter product name">
                </div>
                <div class="form-group">
                    <label for="productPrice">Price:</label>
                    <input type="number" id="productPrice" name="price" required min="0.01" max="1000000" step="0.01" placeholder="0.00">
                </div>
                <button type="submit">Add Product</button>
            </form>
        </div>

        <div class="filter-section">
            <h3>🔍 Filter Products</h3>
            <div class="filter-controls">
                <div class="form-group">
                    <label for="minPrice">Minimum Price:</label>
                    <input type="number" id="minPrice" name="minPrice" min="0" step="0.01" placeholder="0.00">
                </div>
                <button type="button" onclick="filterExpensive()">Filter Expensive</button>
                <button type="button" onclick="loadProducts()">Show All</button>
            </div>
        </div>

        <div class="products-section">
            <h2>Products List</h2>
            <div id="productsList" class="products-list">
                <div class="loading">Loading products...</div>
            </div>
        </div>
    </div>

    <script>
        const API = "https://localhost:5001/api/products";

        // Load products on page load
        window.addEventListener('DOMContentLoaded', () => {
            loadProducts();
        });

        // Handle form submission
        document.getElementById('productForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            
            const name = document.getElementById('productName').value;
            const price = parseFloat(document.getElementById('productPrice').value);

            try {
                const response = await fetch(API, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({ name, price })
                });

                if (response.ok) {
                    showMessage('Product added successfully!', 'success');
                    document.getElementById('productForm').reset();
                    loadProducts();
                } else {
                    const error = await response.json();
                    showMessage(`Error: ${error.title || 'Failed to add product'}`, 'error');
                }
            } catch (error) {
                showMessage(`Error: ${error.message}`, 'error');
            }
        });

        // Load all products
        async function loadProducts() {
            try {
                const response = await fetch(API);
                
                if (!response.ok) {
                    throw new Error('Failed to load products');
                }

                const products = await response.json();
                displayProducts(products);
            } catch (error) {
                showMessage(`Error loading products: ${error.message}`, 'error');
                document.getElementById('productsList').innerHTML = 
                    '<div class="loading">Error loading products. Please check if the API is running.</div>';
            }
        }

        // Filter expensive products
        async function filterExpensive() {
            const minPrice = parseFloat(document.getElementById('minPrice').value);
            
            if (isNaN(minPrice) || minPrice < 0) {
                showMessage('Please enter a valid minimum price', 'error');
                return;
            }

            try {
                const response = await fetch(`${API}/expensive?minPrice=${minPrice}`);
                
                if (!response.ok) {
                    throw new Error('Failed to filter products');
                }

                const products = await response.json();
                displayProducts(products);
                showMessage(`Showing products with price > ${minPrice}`, 'success');
            } catch (error) {
                showMessage(`Error filtering products: ${error.message}`, 'error');
            }
        }

        // Update product price
        async function updatePrice(id, currentPrice) {
            const newPrice = prompt(`Enter new price for this product:`, currentPrice);
            
            if (newPrice === null) {
                return; // User cancelled
            }

            const price = parseFloat(newPrice);
            
            if (isNaN(price) || price < 0.01 || price > 1000000) {
                showMessage('Price must be between 0.01 and 1,000,000', 'error');
                return;
            }

            try {
                const response = await fetch(`${API}/${id}/price?newPrice=${price}`, {
                    method: 'PUT'
                });

                if (response.ok || response.status === 204) {
                    showMessage('Price updated successfully!', 'success');
                    loadProducts();
                } else if (response.status === 404) {
                    showMessage('Product not found', 'error');
                } else {
                    const error = await response.text();
                    showMessage(`Error: ${error || 'Failed to update price'}`, 'error');
                }
            } catch (error) {
                showMessage(`Error: ${error.message}`, 'error');
            }
        }

        // Display products in the list
        function displayProducts(products) {
            const productsList = document.getElementById('productsList');
            
            if (products.length === 0) {
                productsList.innerHTML = '<div class="loading">No products found.</div>';
                return;
            }

            productsList.innerHTML = products.map(product => `
                <div class="product-card">
                    <div class="product-info">
                        <div class="product-name">${escapeHtml(product.name)}</div>
                        <div class="product-price">$${product.price.toFixed(2)}</div>
                    </div>
                    <div class="product-actions">
                        <button class="btn-update" onclick="updatePrice(${product.id}, ${product.price})">Update Price</button>
                    </div>
                </div>
            `).join('');
        }

        // Show message to user
        function showMessage(text, type) {
            const messageDiv = document.getElementById('message');
            messageDiv.textContent = text;
            messageDiv.className = `message ${type} show`;
            
            setTimeout(() => {
                messageDiv.classList.remove('show');
            }, 5000);
        }

        // Escape HTML to prevent XSS
        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }
    </script>
</body>
</html>
```

**⚠️ Important :** Ajustez l'URL de l'API si votre port est différent de 5001 :
```javascript
const API = "https://localhost:VOTRE_PORT/api/products";
```

## ÉTAPE 11.3 : Créer swagger.html (documentation API)
📁 `wwwroot/swagger.html`

**Objectif :**
- Avoir une interface Swagger UI accessible via le navigateur
- Tester tous les endpoints
- Documentation interactive de l'API

**Code complet à copier :**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Swagger UI - DemoApi</title>
    <link rel="stylesheet" type="text/css" href="https://unpkg.com/swagger-ui-dist@5.17.14/swagger-ui.css" />
    <style>
        html {
            box-sizing: border-box;
            overflow: -moz-scrollbars-vertical;
            overflow-y: scroll;
        }
        *, *:before, *:after {
            box-sizing: inherit;
        }
        body {
            margin: 0;
            background: #fafafa;
        }
    </style>
</head>
<body>
    <div id="swagger-ui"></div>
    <script src="https://unpkg.com/swagger-ui-dist@5.17.14/swagger-ui-bundle.js"></script>
    <script src="https://unpkg.com/swagger-ui-dist@5.17.14/swagger-ui-standalone-preset.js"></script>
    <script>
        window.onload = function() {
            // Get the current host and port to build the OpenAPI JSON URL
            const host = window.location.host;
            const protocol = window.location.protocol;
            const openApiUrl = `${protocol}//${host}/openapi/v1.json`;
            
            const ui = SwaggerUIBundle({
                url: openApiUrl,
                dom_id: '#swagger-ui',
                deepLinking: true,
                presets: [
                    SwaggerUIBundle.presets.apis,
                    SwaggerUIStandalonePreset
                ],
                plugins: [
                    SwaggerUIBundle.plugins.DownloadUrl
                ],
                layout: "StandaloneLayout",
                tryItOutEnabled: true
            });
        };
    </script>
</body>
</html>
```

**Explications :**

1. **index.html** :
   - Utilise l'API Fetch pour communiquer avec le backend
   - Affiche les produits dans une interface moderne
   - Permet d'ajouter, filtrer et mettre à jour les prix
   - Gestion d'erreurs avec messages utilisateur

2. **swagger.html** :
   - Charge Swagger UI depuis un CDN
   - Récupère automatiquement la spécification OpenAPI depuis `/openapi/v1.json`
   - Permet de tester tous les endpoints directement dans le navigateur

**Accès :**
- Frontend : `https://localhost:5001/index.html`
- Swagger UI : `https://localhost:5001/swagger.html`
- OpenAPI JSON : `https://localhost:5001/openapi/v1.json`

---

# PARTIE 12 : LANCER ET TESTER L'APPLICATION

## ÉTAPE 12.1 : Lancer l'application
1. Dans Visual Studio, appuyez sur **F5** ou cliquez sur le bouton vert **Démarrer**
2. Le navigateur s'ouvrira automatiquement (généralement sur `https://localhost:5001`)

3. Si vous voyez une erreur de certificat SSL :
   - Cliquez sur **"Avancé"**
   - Cliquez sur **"Continuer vers localhost (non sécurisé)"**

## ÉTAPE 12.2 : Tester les endpoints
Vous pouvez tester votre API de plusieurs façons :

### 1. Via Swagger UI
- Naviguez vers : `https://localhost:5001/swagger.html`
- Vous verrez tous vos endpoints
- Vous pouvez les tester directement dans le navigateur

### 2. Via l'interface HTML
- Naviguez vers : `https://localhost:5001/index.html`
- Ajoutez des produits
- Visualisez la liste
- Filtrez les produits chers

### 3. Via Postman ou un autre client HTTP
- `GET https://localhost:5001/api/products`
- `POST https://localhost:5001/api/products`
  - Corps JSON : `{ "name": "Laptop", "price": 999.99 }`

### 4. Via le navigateur
- Ouvrez directement : `https://localhost:5001/api/products`
- Vous verrez le JSON directement

**⚠️ Note :** Si votre port est différent de 5001, vérifiez dans `Properties/launchSettings.json` et ajustez les URLs en conséquence.

---

# PARTIE 13 : DÉBOGUAGE (RÉSOLUTION DE PROBLÈMES)

## PROBLÈME 1 : Erreur de connexion à la base de données
**Erreur :** "A network-related or instance-specific error occurred..."

**Solutions :**
1. Vérifiez que SQL Server LocalDB est installé
   - Ouvrez SQL Server Management Studio
   - Essayez de vous connecter à `(localdb)\mssqllocaldb`

2. Vérifiez la chaîne de connexion dans `appsettings.json` :
   ```json
   "Server=(localdb)\\mssqllocaldb;..."
   ```
   Le double backslash `\\` est obligatoire.

3. Vérifiez que vous avez bien exécuté `Update-Database`

## PROBLÈME 2 : Migration déjà existante
**Erreur :** "The migration 'InitialCreate' already exists"

**Solution :**
1. Dans la Console du Gestionnaire de packages :
   ```powershell
   Remove-Migration
   ```
2. Puis recréez la migration :
   ```powershell
   Add-Migration InitialCreate
   Update-Database
   ```

## PROBLÈME 3 : Port déjà utilisé
**Erreur :** "Unable to bind to https://localhost:5001"

**Solution :**
1. Modifiez `Properties/launchSettings.json`
2. Changez le port dans `"applicationUrl"`
3. Mettez à jour l'URL dans `wwwroot/index.html` (variable `API`)

## PROBLÈME 4 : Erreur CORS
**Erreur :** "Access to fetch at '...' from origin '...' has been blocked by CORS policy"

**Solution (si vous testez depuis un autre site) :**
Dans `Program.cs`, ajoutez :
```csharp
builder.Services.AddCors(options =>
{
    options.AddDefaultPolicy(policy =>
    {
        policy.AllowAnyOrigin()
              .AllowAnyMethod()
              .AllowAnyHeader();
    });
});

// Et dans le pipeline :
app.UseCors();
```

## PROBLÈME 5 : Warning sur la précision décimale
**Warning :** "No store type was specified for the decimal property 'Price'"

**Solution :**
C'est déjà résolu ! On a ajouté `HasPrecision(18, 2)` dans `AppDbContext.OnModelCreating`.

## PROBLÈME 6 : Swagger UI ne s'affiche pas
**Solution :**
1. Vérifiez que `app.MapOpenApi()` est présent dans `Program.cs`
2. Vérifiez que le fichier `wwwroot/swagger.html` existe
3. Accédez à `https://localhost:5001/swagger.html` (pas `/swagger`)

---

# PARTIE 14 : CONCEPTS CLÉS À RETENIR
MVC, Services, DI, Async/Await, EF Core, migrations, REST, Status Codes.

---

# PARTIE 15 : PROJET FINAL (BACKEND + FRONTEND + BONUS)

## 15.1 : API Fournisseurs (Supplier)
Attendus :
- Ajouter un fournisseur
- Voir les fournisseurs
- Modifier les fournisseurs
Tout pareil que Product.

## 15.2 : API Matières Premières (RawMaterial)
Attendus :
- Créer / modifier / afficher
Tout pareil que Product.

## 15.3 : BONUS — Relations + recherche de produits
Objectif : faire le lien entre les models et permettre la recherche :
- Produit à partir d’un fournisseur
- Produit à partir d’une matière première

Routes attendues :
- `GET /api/products/by-supplier/{supplierId}`
- `GET /api/products/by-rawmaterial/{rawMaterialId}`

---

# RESSOURCES POUR ALLER PLUS LOIN
- ASP.NET Core : https://learn.microsoft.com/fr-fr/aspnet/core/
- Entity Framework Core : https://learn.microsoft.com/fr-fr/ef/core/
- C# : https://learn.microsoft.com/fr-fr/dotnet/csharp/

---

# CONCLUSION
Félicitations ! Vous avez créé une API complète avec :
- SQL Server + EF Core
- Controllers REST
- Services + DI
- Frontend HTML/JS
- Swagger obligatoire

Bon courage 🚀
