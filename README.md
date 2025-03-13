<h1>Sort My Object</h1>

<h2>Description</h2>
The **Sort My Object** project is a Java program that allows users to create and manage a list of songs. The program enables users to input song details, store them in an <code>ArrayList</code>, and sort them based on different properties using <code>Comparator</code> and <code>Comparable</code> interfaces.

This project demonstrates **object-oriented programming (OOP) principles**, **user input handling**, **file writing**, and **sorting using Comparators**.

<br />

<h2>Languages and Tools Used</h2>

- <b>Java</b>
- <b>ArrayList</b> (for storing objects)
- <b>Scanner Class</b> (for user input)
- <b>FileWriter</b> (for saving playlist data)
- <b>Comparators</b> (for sorting objects)

<h2>Program Walk-through</h2>

1. **User Input and Object Creation**:
   - The user specifies how many songs they want to add.
   - For each song, the user provides:
     - **Title**
     - **Artist**
     - **Genre**
   - Each song is stored as a `Song` object inside an `ArrayList<Song>`.

2. **Displaying and Saving Songs**:
   - The program prints the list of songs entered.
   - The songs are saved to a file named <code>PlayList.txt</code>.

3. **Sorting the Song List**:
   - The user can choose to sort the playlist **by Title** or **by Artist**.
   - The program uses `Comparator<Song>` implementations to sort based on the selected property.
   - The sorted list is displayed after sorting.

<h2>Example Code</h2>

```java
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.Scanner;

class Song {
    private String title;
    private String artist;
    private String genre;

    public Song(String title, String artist, String genre) {
        this.title = title;
        this.artist = artist;
        this.genre = genre;
    }

    public String getTitle() { return title; }
    public String getArtist() { return artist; }
    public String getGenre() { return genre; }

    @Override
    public String toString() {
        return title + " - " + artist + " (" + genre + ")";
    }
}

public class SortMyObject {
    public static void main(String[] args) {
        Scanner keyboard = new Scanner(System.in);
        ArrayList<Song> mySongs = new ArrayList<>();

        // User input for songs
        System.out.print("How many songs would you like to add? ");
        int numSongs = Integer.parseInt(keyboard.nextLine());

        for (int i = 0; i < numSongs; i++) {
            System.out.print("Enter song title: ");
            String title = keyboard.nextLine();

            System.out.print("Enter artist: ");
            String artist = keyboard.nextLine();

            System.out.print("Enter genre: ");
            String genre = keyboard.nextLine();

            mySongs.add(new Song(title, artist, genre));
        }

        // Save songs to file
        try {
            FileWriter myWriter = new FileWriter("PlayList.txt");
            for (Song song : mySongs) {
                myWriter.write(song + "\n");
            }
            myWriter.close();
            System.out.println("Playlist saved to PlayList.txt");
        } catch (IOException e) {
            System.out.println("Error writing to file.");
        }

        // Comparators for sorting
        Comparator<Song> compareByTitle = Comparator.comparing(Song::getTitle);
        Comparator<Song> compareByArtist = Comparator.comparing(Song::getArtist);

        while (true) {
            System.out.println("\nCurrent Playlist:");
            for (Song song : mySongs) {
                System.out.println(song);
            }

            System.out.println("\nHow would you like to sort your playlist?");
            System.out.println("Options: Title | Artist");
            String sortBy = keyboard.nextLine();

            if (sortBy.equalsIgnoreCase("Title")) {
                Collections.sort(mySongs, compareByTitle);
            } else if (sortBy.equalsIgnoreCase("Artist")) {
                Collections.sort(mySongs, compareByArtist);
            } else {
                System.out.println("Invalid option. Try again.");
                continue;
            }

            System.out.println("\nSorted Playlist:");
            for (Song song : mySongs) {
                System.out.println(song);
            }
        }
    }
}
