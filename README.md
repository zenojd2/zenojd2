👋 Hi,  My name Javian Zeno and this is my awesome Counting Numbers Project.

package countwords;

import java.io.File;

import java.io.FileNotFoundException;

import java.io.FileOutputStream;

import java.io.PrintWriter;

import java.util.Arrays;

import java.util.Scanner;

/**

*Class name: CountWords

* Description: Gets a file path from user and counts the unique words and writes into a text file

* @author sachinna

*/

public class CountWords {

    //Let define the array size as 100

    final static int ARRAY_WORDS_SIZE = 100;

    //Define the output file path

    final static String OUTPUT_FILE_PATH = "UniqueWords.txt";

   

    /**

     * @param args the command line arguments

     */

    public static void main(String[] args) {      

        Scanner scanInputFile = null;

        try {

             //Get the file name

            System.out.println("Enter the input File Name:");

            Scanner keyboard = new Scanner(System.in);

            String inputfilepath = keyboard.nextLine();

            //String inputfilepath = "C:\\Data\\Java.txt";

           

            scanInputFile = new Scanner(new File(inputfilepath), "UTF-8");

        } catch (FileNotFoundException e) {

            //print if any error and exit

            System.err.println("Error opening file. " + e.getMessage());

            System.exit(1);

        }

       

        //Declare two arrays to store uniqueWords and their count

        int[] uniqueWordsCount = new int[ARRAY_WORDS_SIZE];

        String[] uniqueWords = new String[ARRAY_WORDS_SIZE];

        //To track unique word count

        int uniqueWordCount = 0;

       

        //Iterate through lines

        while (scanInputFile.hasNextLine()) {

            //For each line get the words

            Scanner scanWords = new Scanner(scanInputFile.nextLine());

            //for each word

            while (scanWords.hasNext()) {

                String word = scanWords.next();

                //Remove Punctuation marks from the word

                word = word.replaceAll("\\p{Punct}", "");

                int wordFound = Arrays.asList(uniqueWords).indexOf(word);

                //If already exists in the array

                if(wordFound > -1){

                    //Increase the corresponding count

                    uniqueWordsCount[wordFound]++;

                }

                else{

                    if(uniqueWordCount < ARRAY_WORDS_SIZE )

                    {

                        //Add the word to uniqueWords array and make the count to 1

                        uniqueWords[uniqueWordCount] = word;

                        uniqueWordsCount[uniqueWordCount] = 1;

                        uniqueWordCount++;

                    }

                }

            }

        }

      

        try ( //write the results into file

                PrintWriter fileResult = new PrintWriter(new FileOutputStream(OUTPUT_FILE_PATH))) {

            int i = 0;

            // traverse in the arrays

            while (i < uniqueWordCount) {

                //write in the output file in two columns

                fileResult.println(String.format( "%15s %-8s", uniqueWords[i], uniqueWordsCount[i]));

                i++;

            }

        }catch (FileNotFoundException e) {

            System.err.println("Error writing output file. " + e.getMessage());

            System.exit(1);

        }

    }       

}

