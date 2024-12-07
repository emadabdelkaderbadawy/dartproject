# dartproject
this is my new repository
import 'dart:io';

void main() {
  List<Map<String, dynamic>> inventory = [];
  bool running = true;

  while (running) {
    print('Menu:');
    print('1. Add Book');
    print('2. View All Books');
    print('3. Search by Genre');
    print('4. Exit');
    stdout.write('Choose an option (1-4): ');

    String? choice = stdin.readLineSync();

    switch (choice) {
      case '1':
        addBook(inventory);
        break;
      case '2':
        viewAllBooks(inventory);
        break;
      case '3':
        searchByGenre(inventory);
        break;
      case '4':
        running = false;
        break;
      default:
        print('Invalid option. Please try again.');
    }
  }
}

bool addBook(List<Map<String, dynamic>> inventory) {
  stdout.write('Enter book title: ');
  String? title = stdin.readLineSync();
  stdout.write('Enter book author: ');
  String? author = stdin.readLineSync();
  stdout.write('Enter book genres (comma separated, leave blank for none): ');
  String? genresInput = stdin.readLineSync();

  Set<String> genres = <String>{};
  if (genresInput != null && genresInput.isNotEmpty) {
    genres.addAll(genresInput.split(',').map((genre) => genre.trim()).toSet());
  }

  if (title != null && author != null) {
    Map<String, dynamic> newBook = {
      'title': title,
      'author': author,
      'genres': genres,
    };
    inventory.add(newBook);
    print('Book added successfully.');
    return true;
  } else {
    print('Title and author cannot be empty.');
    return false;
  }
}

void viewAllBooks(List<Map<String, dynamic>> inventory) {
  if (inventory.isEmpty) {
    print('No books   found.');
  } else {
    inventory.forEach((book) {
      print('Title: ${book['title']}, Author: ${book['author']}, Genres: ${book['genres'].join(', ')}');
    });
  }
}

void searchByGenre(List<Map<String, dynamic>> inventory) {
  stdout.write('Enter genre to search: ');
  String? genre = stdin.readLineSync();

  if (genre != null && genre.isNotEmpty) {
    List<Map<String, dynamic>> foundBooks = inventory.where((book) => book['genres'].contains(genre)).toList();

    if (foundBooks.isEmpty) {
      print('No books found for genre: $genre');
    } else {
      foundBooks.forEach((book) {
        print('Title: ${book['title']}, Author: ${book['author']}, Genres: ${book['genres'].join(', ')}');
      });
    }
  } else {
    print('Genre cannot be empty.');
  }
}
