# Entretien technique C\#

1. Quelles sont les différents types de classe qui existent en C\#

> **Static**: C'est un type de classe qui ne peut pas être instancier, on ne peut pas créer des objets de ce type en utilisant le mot clé **new**. On appelle les membres directement à partir du nom de la classe.
> **Abstract**: On ne peut pas créer des objects de ce type directement, il faut nécessairement hériter de cette classe pour l'instancier. Les méthodes de cette classes peuvent être abstraites ou non.
> **Partial**: C'est un type de classe qui autorise la division des propriétés, méthodes et événements dans plusieurs fichiers sources. Les fichiers sont combinées en une classe unique au moment de la compilation.
> **Sealed**: Aucune classe ne peut en hériter.

2. Quelle est la différence entre **break** et **continue**? Est-ce qu'on peut utiliser **break** dans un **if**? Pareil mais pour **continue**?

> **break** peut s'utiliser dans les switch et les boucles, quand le mot clé est atteint, le switch ou la boucle est interrompu. Dans le cas de boucles imbriquées seule la boucle englobante est interrompue.
> **continue** ne s'utilise que dans les boucles, il interrompt le tour de boucle courant pour passer au prochain tour sans exécuter le code immédiat après lui.

3. Qu'est-ce qu'une surcharge de méthode?

> C'est une technique qui permet aux développeurs d'utiliser plusieurs méthodes du même nom mais avec un nombre et des types différents de paramètres. C'est basé sur le polymorphisme. On peut donc changer le nombre de paramètres passés, changer l'ordre ou même changer de types.

4. C'est quoi le boxing et l'unboxing?

> **Boxing**: Le processus qui consiste à convertir une variable de type valeur à un type référence, il est donc stocké dans le tas. C'est une conversion implicite car en C# tout est de type **Object**
>
> ```csharp
> int a = 1;
> object boxed_a = a;
> ```
> **Unboxing**: c'est le processus inverse qui consiste donc à transférer un objet dans la pile grâce à une conversion explicite dans l'objet de type valeur.
>
> ```csharp
> object boxed_a = 2;
> int a = (int)boxed_a;
> ```

5. Quelle sont les différences entre les types référence et les types valeur?

> Les objets de type valeurs sont stockés dans la pille (stack)
> Les objets de type référence sont stockés dans le tas (heap)

6. Quelle est la différence entre le passage par référence et le passage par valeur?

> Le passage par référence permet à une méthode de copier la référence de l'objet qu'on lui passe et donc toute modification dans la méthode, change la valeur de l'objet en dehors de la méthode.
> Le passage par valeur permet à une méthode de copier la valeur de l'objet et non pas la référence. La méthode travaille donc sur une copie de l'objet. Les 2 copies de la variable sont dissociées. Modifier la copie locale ne change pas la valeur de l'objet en dehors de la méthode.

7. Quelles sont les techniques pour fabriquer un type **delegate**? Quelle est la différence entre les **Action** et les **Func**

> Les **delegate** sont comme des pointeurs de fonction qui gardent la référence d'une méthode.
> Utiliser le mot clé **delegate**
>
> ```csharp
> public delegate int CalculatorDelegate(int a, int b);
> CalculatorDelegate caclOperation = (a, b) => a + b;
> ```
>
> Utiliser les mots clés **Action** et **Func**. **Action** est un type **delegate** qui prend en entrée un nombre variable de paramètres et qui ne retourne rien (void). **Func** lui est l'équivalent du type **Action** mais qui retourne une valeur.
>
> ```csharp
> Action<int> Method = (x) => Console.WriteLine(x);
> Func<int, int, string> Method = (a, b) => string.Format("{0} et {1} sont des entiers", a, b);
> ```

8. C'est quoi la Réflection en C\#?

> C'est la capacité du code à accéder aux metadata de l'assembly pendant le runtime. Il permet de récupérer le type des objets d'identifier des membres d'un objet, les méthodes etc...

9. Connaissez vous les expressions régulières?

> C'est un système de template pour trouver les correspondances entre un set d'entrée et un pattern. C'est une construction de caractères et d'opérateurs qui permet de généraliser la recherche dans une chaine de caractères.

10. Qu'est-ce que la sérialisation en C\#?

> C'est le processus qui consiste à convertir du code en format binaire. Par exemple convertir des données en fichier texte json

11. A quoi sert le mot clé **this**? Peut-on l'utiliser dans une méthode statique?

> Le mot clé **this** sert à accéder à la référence de l'objet courant et donc impossible à utiliser dans une méthode statique. Cette dernière n'a pas besoin d'instance de classe pour exister et donc son référencement n'a pas de sens. Cependant on peut l'utiliser en tant que paramètre d'une méthode d'extension

12. A quoi servent et comment fonctionnent **async** et **await**?

> Ils s'utilisent pour faire de la programmation asynchrone. Le processus principal lance le main et quand il atteint une demande **await**, la fonction rend la main au processus principal pendant qu'un process secondaire se charge de traiter la demande marquée par **await**. Une fois que le résultat est renvoyé, le processus secondaire prend la main pour retourner le résultat attendu.

13. Qu'est-ce qu'une condition de concurrence ou race condition?

> C'est quand plusieurs thread essayent d'accéder à une même ressource tout en y opérant des modifications, il est quasiment impossible de déterminer lequel des thread prendra la mainen premier. Le thread qui arrivera en dernier décidera de la valeur à associer à la ressource.

14. En C\#9+ il existe une nouvelle structure en plus de **class** et **struct**. A quoi sert-elle principalement?

> **record** est un nouveau mot clé qu'on utilise pour définir des nouvelles structures destinées à encapsuler les données.
> Les *positional record* et *positional readonly record struct* sont par défaut immuables

15. Comment vous créez une méthode d'extention d'un **Type générique T de type valeur**

> ```csharp
> public static class Extension
> {
>   public static T  Method<T>(this T myInt) 
>       where T : struct
>   {
>       // Do your thing
>   }
> }
> ```
>
> ```csharp
> public static class Extension
> {
>   public static T Method<T , U>(this T myInt, U optionalParams) 
>       where T : struct
>       where U : class
>   {
>       // Do your thing
>   }
> }
> ```

16. Est-ce que le C# c'est du code managé ou justement non managé?

> C'est du code managé, le CLR (Common Language Runtime) le converti en code intermédiaire.

17. Quelle est la différence entre **const** et **readonly**?

> Les variables constantes ne peuvent être assignés qu'à la déclaration et ne peuvent changer de valeur.
> Les variables readonly ne peuvent assignés que dans le constructeur de la classe dans laquelle ils se trouvent, mais il est possible de modifier les valeurs contenues mais pas de les réassigner. (on peut ajouter des valeurs dans une liste mais pas réassigner la référence de la liste).

18. Quelle est la différence entre **string** et **StringBuilder**?

> **string** est immuable donc quand des actions visent à modifier la chaîne, en réalité une nouvelle chaîne est crée et l'ancienne valeur est oubliée.
> **StringBuilder** permet de faire des opérations de concaténation et de remplacement tout en gagnant de la performance. En effet c'est un objet modifiable il possible de choisir de construire un **string** uniquement à la fin de toutes les opérations.

19. Qu'est ce que l'injection de dépendance en C\#?

> C'est un design pattern qui consiste à passer une instance d'un objet A à une classe B au lieu de créer un objet A pour une autre classe B à chaque fois. Ca permet d'assouplir le couplage du code. Et donc à le rendre plus modulaire et à faciliter les tests.