# SEKY - Search keywords in several PDFs at once.
  #### Video Demo:  <https://youtu.be/VHVpPTiUyWo>
  #### Description:

    The goal of this software is to search for keywords in one or more PDFs at the same time. The following explains how it works:

    The user is asked for the path directory where the PDFs in which he wishes to search are stored:
    *If the path provided by the user is incorrect or omitted (by pressing enter) the software will re-request the path.
    *If there are no pdf files in the path indicated by the user, the software will print on the screen that there are not PDF 
    files but it will not request the path again.

    The user is requested to type the keywords separated by spaces:
    *If the user enters the keywords without spaces the software has no way to separate the words. 
    *If the user does not provide the keywords (by pressing enter) the program will request the keywords again.

    The software gets a list of all files in the path specified by the user. The software filters the files and keeps the pdf 
    files only, storing them internally in a list. For each PDF file in the list the software will extract the text contained 
    in it. For this task, two modules are used depending on whether the PDF can be read or not:
    *The [fitz](https://pymupdf.readthedocs.io/en/latest/module.html) module has been used for readable PDFs.
    *The [python-tesseract](https://pypi.org/project/pytesseract/) is a wrapper for Google’s Tesseract-OCR. It has been used
    for extracting text for the non-readables PDF (previously converted to an image with the fizt module).
    
    The text obtained from the PDF is transformed into a list where each element is a word. As the words obtained by the OCR tool
    can have errors, a parameter has been used to measure the similarity with the keywords. 
    A [Levenshtein distance](https://maxbachmann.github.io/Levenshtein/) of less than 40 percent of the word length has been chosen.

    Keywords that match or are similar to the words in the PDF under analysis are stored internally in a list. All keywords are 
    expected to be found. If not, the name of that PDF will not be printed on the screen nor stored in an XLS file.

    If the keywords are not found in any of the PDFs, the software will print on the screen to be tested with other keywords. 
    However, it will not request the keywords to be entered again. If the user wants to, he must run the program again.

    If at least one PDF contains all the keywords (or similar words), the software will print the name of that PDF file on the screen
    and notify the user that the results have been saved to an XLS file in the path where the PDFs are stored. 
    The [openpyxl](https://openpyxl.readthedocs.io/en/stable/) library has been used to write the output in an excel workbook.

    Below is a description some of the functions called for the main function:
    
    *The following function returns a list of the key words (splited by space)
    ```
    get_keywords()
    ```
    *The following function returns a list of the PDFs founded in the path provided by the user.
    ```
    get_pdf_ls()
    ```
    *The following function return a list of the words detected in each PDF.
    ```
    get_str_ls(pdf, dir_path)
    ```
    *The following function returns a list of the keywords found in the list of words detected in the PDF.
    ```
    get_matches_ls(str_ls, key_words)
    ```
    *The following function returns a string that contains the names and the amount of the PDFs that matches all the keywords. Also, it returns a workbook with those names (one per row).
    ```
    get_output(pdf_ls, key_words, dir_path)
    ```
