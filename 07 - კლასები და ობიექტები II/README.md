## toString მეთოდი

წინა გაკვეთილში განვიხილეთ მარტივი Rectangle კლასი:

```dart

void main() {
    Rectangle rect = Rectangle(3,5);
    print(rect);
}

class Rectangle {
    double side1 = 0;
    double side2 = 0;

    Rectangle(double a, double b) {
        side1 = a;
        side2 = b;
    }

    double calculatePerimeter() {
        return 2 * (side1 + side2);
    }
}

```

ამ მაგალითის main ფუნქციაში ჩვენ შევქმენით ობიექტი Rectangle კლასისაგან და შემდეგ ვცადეთ ამ ობიექტის print ფუნქციისათვის გადაცემა.
პროგრამის გაშვების შემდეგ კონსოლში დაიბეჭდა : Instance of 'Rectangle'. ეს მესიჯი გვამცონბს, რომ ობიექტი რომელიც print ფუნქციას გადეცა არის Rectangle მონაცემის ტიპის. ეს ინფორმაცია არც ისე გამოსადეგია ამიტომ ვნახოთ როგორ შეგვიძლია შევცვალოთ ეს ფუნქციონალი. ამისთვის შეგვიძლია გამოვიყენოთ toString მეთოდი (რომელიც ყველა კლასს აქვს და თუ რატომ შემდეგ გაკვეთილში ვნახავთ). მოდით დავამატოთ toString მეთოდი ჩვენს Rectangle კლასს

```dart

void main() {
    Rectangle rect = Rectangle(3,5);
    print(rect);
}

class Rectangle {
    double side1 = 0;
    double side2 = 0;

    Rectangle(double a, double b) {
        side1 = a;
        side2 = b;
    }

    double calculatePerimeter() {
        return 2 * (side1 + side2);
    }

    String toString() {
        return 'Rectangle{side1: $side1, side2: $side2}';
    }
}

```

ამ პროგრამის გაშვების შემდეგ კონსოლში დაიბეჭდება: 

Rectangle{side1: 3, side2: 5}

toString მეთოდი საშვალებას გვაძლევს ვნახოთ თუ რა არის ობიექტის ტექსტური რეპრეზენტაცია. იმის მიუეხდავად, რომ toString მეთოდის default ფუნქციონალი არც ისე სასარგებლოა ჩვენ შეგვიძლია შევცვალოთ ამ ფუნქციის დასაბრუნებელი მნიშვნელობა და დავაბრუნოთ ჩვენი პროგრამისათვის საჭირო ინფორმაცია. როგორც წესი ეს კლასის ცვლადების სახელები და მათი მნიშვნელობებია. ამ მაგალითში მოცემული ფორმატი არ არის სავალდებულო თუმცა გახლავთ დარტის სტანდარტი და მსგავს მაგალითებს ხშირად შევხვდებით.


## კლასების გამოყენების პრაქტიკული მაგალითი

ამ გაკვეთილში შევქმნით ეგრედწოდებულ TO-DO პროგრამას, რომელშიც შეგვეძლება დავამატოთ ახალი ელემენტები, წავშალოთ ელემენტები და ასევე კონსოლში ყველა ელემენიტი. სანამ პროგრამის წერას შევუდგებით დავფიქრდეთ, რომელი ობიექტების აღწერა გამოგვადგება. ამ პროგრამის შექმნა ბევრი სხვადასხვა გზით შეიძლება, თუმცა პროგრამის აღწერას თუ გადავხედავთ კარგი იქნება თუ გვექნება ერთი კლასი TO-DO ელემენტებისათვის და ერთი კლასი ყველა ელემენტის შესანახად. ამ უკანასკნელში გვექნება ელემენტების დამატების, წაშლის და კონსოლში დაბეჭდვის ფუნქციონალი. მოდი პირველ რიგში შევქმნათ TO-DO კლასი:

```dart

class TodoItem {
    String title;
    String description;

    TodoItem({required this.title, required this.description});

    String toString() {
        return 'TodoItem{title: $title, description: $description}';
    }
}

```

ზემოთ შექმნილ კლასში გვაქვს ორი ცვლადი TO-DO ელემენტის აღსაწერად სათაური და მოკლე აღწერა. კონსტრუქტორში კი სწორად ამ ინფორმაციებს მივიღებთ. ასევე გვაქვს toString მეთოდი. ახლა კი მოდით შევქმნათ ჩვენი მთავარი კლასი რომელშიც შევინახავთ ჩვენს TO-DO ელემენტებს (TodoItem - ობიექტებს).

```dart

class TodoList {
    List<TodoItem> todoItems = [];


    void addTodo(TodoItem todoItem) {
        todoItems.add(todoItem);
    }

    void removeTodo(TodoItem todoItem) {
        todoItems.remove(todoItem);
    }

    void printTodoList() {
        for(int i = 0; i < todoItems.length; i++) {
            print('${todoItems[i]}');
        }
    }
}

```

TodoList კლასში ჩვენ გვაქვს: 
 - todoItems ცვლადი, რომლის მონაცემის ტიპი არის სია (ხოლო სიის ელემენტები არის TodoItem მონაცემის ტიპის).
 - todoItems ცვლადს ვანიჭებთ default მნიშვნელობას (ცარიელ სიას)
 - addTodo მეთოდი
 - removeTodo მეთოდი
 - printTodoList მეთოდი

მოდით ახლა გამოვიყენოთ ჩვენს მიერ შექმნილი კლასები main ფუნქციაში და ვნახოთ თუ როგორ მუშაობს ჩვენს მიერ აღწერილი ფუნქციონალი.

```dart

void main() {
  TodoItem todo1 = TodoItem(title: 'learn dart', description: 'read lecture 7');
  
  TodoItem todo2 = TodoItem(title: 'Quizz', description: 'prepare for Quizz');
  
  TodoItem todo3 = TodoItem(title: 'exercise', description: 'Do 10 push-ups');
  
  TodoList todos = TodoList();
  todos.addTodo(todo1);
  todos.addTodo(todo2);
  todos.addTodo(todo3);
  todos.displayTodoList();
  todos.removeTodo(todo3);
  todos.displayTodoList();
  
}

class TodoItem {
  String title;
  String description;

  TodoItem({required this.title, required this.description});

  String toString() {
    return 'TodoItem{title: $title, description: $description}';
  }
}

class TodoList {
  List<TodoItem> todoItems = [];

  void addTodo(TodoItem todoItem) {
    todoItems.add(todoItem);
  }

  void removeTodo(TodoItem todoItem) {
    todoItems.remove(todoItem);
  }

  void displayTodoList() {
    for (int i = 0; i < todoItems.length; i++) {
      print('${todoItems[i]}');
    }
  }
}

```

ზემოთ მოცემული პროგრამის გაშვების შემდეგ კონსოლში დაიბეჭდება:

TodoItem{title: learn dart, description: read lecture 7}
TodoItem{title: Quizz, description: prepare for Quizz}
TodoItem{title: exercise, description: Do 10 push-ups}
--------------------------
TodoItem{title: learn dart, description: read lecture 7}
TodoItem{title: Quizz, description: prepare for Quizz}

პროგრამის main ფუნქციაში ჩვენ:
- შევქმენით სამი TodoItem ობიექტი
- შევქმენით TodoList ობიექტი
- TodoList ობიექტში დავამატეთ სამი ცალი TodoItem ობიექტი addTodo მეთოდის გამოყენებით
- დავბეჭდეთ TodoList ობიექტში შენახული ელემენტები(TodoItem_ები)
- TodoList ობიექტიდან წავშალეთ ერთერთი TodoItem
- თავიდან დავბეჭდეთ TodoList ობიექტში შენახული ელემენტები(TodoItem_ები)

პროგრამის გაშვების შემდეგ ვნახეთ, რომ ჩვენს მიერ შექმნილ კლასებს ყველა ის ფუნქციონალი აქვს, რომელიც 'ნამდვილ' Todo ტიპის აპლიკაციას ექნებოდა.
რათქმაუნდა მომხმარებელი ვერ შეძლებს ჩვენი აპლიკაციის მოხმარებას main ფუნქციის გამოყენებით. თუმცა მას შემდეგ რაც Flutter ის დახმარებით შევისწავლით მობილური აპლიკაციების შექმნის საფუძვლებს, შეგვეძლება გამოვიყენოთ ჩვენს მიერ შექმნილი TodoItem და TodoList კლასები და შევქმნათ აპლიკაცია, რომელიც ფუნქციურად იდენტური იქნება იმ აპლიკაციებისა, რომლებსაც მაგალითად Google play store ში გადმოწერდით

