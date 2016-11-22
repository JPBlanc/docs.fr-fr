---
title: "Comment&#160;: impl&#233;menter une classe Lightweight avec des propri&#233;t&#233;s impl&#233;ment&#233;es automatiquement (Guide de programmation&#160;C#) | Microsoft Docs"
ms.custom: ""
ms.date: "11/17/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "propriétés implémentées automatiquement (C#)"
  - "propriétés (C#), implémentées automatiquement"
ms.assetid: 1dc5a8ad-a4f7-4f32-8506-3fc6d8c8bfed
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
translationtype: Human Translation
---
# Comment&#160;: impl&#233;menter une classe Lightweight avec des propri&#233;t&#233;s impl&#233;ment&#233;es automatiquement (Guide de programmation&#160;C#)
Cet exemple montre comment créer une classe légère immuable qui sert uniquement à encapsuler un jeu de propriétés implémentées automatiquement.  Utilisez ce type de construction à la place d'un struct quand vous devez utiliser une sémantique de type de référence.  
  
 Vous pouvez rendre une propriété immuable de deux manières.  Vous pouvez déclarer que l'accesseur [set](../../../csharp/language-reference/keywords/set.md) est [privé](../../../csharp/language-reference/keywords/private.md).  La propriété peut uniquement être définie dans le type, mais elle est immuable pour les consommateurs.  Vous pouvez autrement déclarer uniquement l'accesseur [get](../../../csharp/language-reference/keywords/get.md), ce qui rend la propriété immuable partout sauf dans le constructeur du type.  
  
 Quand vous déclarez un accesseur `set` privé, vous ne pouvez pas utiliser un initialiseur d'objet pour initialiser la propriété.  Vous devez utiliser un constructeur ou une méthode de fabrique.  
  
## Exemple  
 L'exemple suivant montre deux façons d'implémenter une classe immuable qui possède des propriétés implémentées automatiquement.  Chaque façon déclare l'une des propriétés avec un `set` privé et l'autre avec un `get` uniquement.  La première classe utilise un constructeur uniquement pour initialiser les propriétés et la deuxième classe utilise une méthode de fabrique statique qui appelle un constructeur.  
  
```c#  
// This class is immutable. After an object is created,   
    // it cannot be modified from outside the class. It uses a   
    // constructor to initialize its properties.   
    class Contact  
    {  
        // Read-only properties.   
        public string Name { get; }  
        public string Address { get; private set; }  
  
        // Public constructor.   
        public Contact(string contactName, string contactAddress)  
        {  
            Name = contactName;  
            Address = contactAddress;                 
        }  
    }  
  
    // This class is immutable. After an object is created,   
    // it cannot be modified from outside the class. It uses a   
    // static method and private constructor to initialize its properties.      
    public class Contact2  
    {  
        // Read-only properties.   
        public string Name { get; private set; }  
        public string Address { get; }  
  
        // Private constructor.   
        private Contact2(string contactName, string contactAddress)  
        {  
            Name = contactName;  
            Address = contactAddress;                 
        }  
  
        // Public factory method.   
        public static Contact2 CreateContact(string name, string address)  
        {  
            return new Contact2(name, address);  
        }  
    }  
  
    public class Program  
    {   
        static void Main()  
        {  
            // Some simple data sources.   
            string[] names = {"Terry Adams","Fadi Fakhouri", "Hanying Feng",   
                              "Cesar Garcia", "Debra Garcia"};  
            string[] addresses = {"123 Main St.", "345 Cypress Ave.", "678 1st Ave",  
                                  "12 108th St.", "89 E. 42nd St."};  
  
            // Simple query to demonstrate object creation in select clause.   
            // Create Contact objects by using a constructor.   
            var query1 = from i in Enumerable.Range(0, 5)  
                        select new Contact(names[i], addresses[i]);  
  
            // List elements cannot be modified by client code.   
            var list = query1.ToList();  
            foreach (var contact in list)  
            {  
                Console.WriteLine("{0}, {1}", contact.Name, contact.Address);  
            }  
  
            // Create Contact2 objects by using a static factory method.   
            var query2 = from i in Enumerable.Range(0, 5)  
                         select Contact2.CreateContact(names[i], addresses[i]);  
  
            // Console output is identical to query1.   
            var list2 = query2.ToList();  
  
            // List elements cannot be modified by client code.   
            // CS0272:   
            // list2[0].Name = "Eugene Zabokritski";   
  
            // Keep the console open in debug mode.  
            Console.WriteLine("Press any key to exit.");  
            Console.ReadKey();                  
        }  
    }  
  
/* Output:  
    Terry Adams, 123 Main St.  
    Fadi Fakhouri, 345 Cypress Ave.  
    Hanying Feng, 678 1st Ave  
    Cesar Garcia, 12 108th St.  
    Debra Garcia, 89 E. 42nd St.  
*/  
  
```  
  
 Le compilateur crée des champs de stockage pour chaque propriété implémentée automatiquement.  Les champs ne sont pas accessibles directement à partir du code source.  
  
## Voir aussi  
 [Propriétés](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [struct](../../../csharp/language-reference/keywords/struct.md)   
 [Initialiseurs d'objets et de collections](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)