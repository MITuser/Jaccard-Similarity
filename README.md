# Jaccard-Similarity

import tkinter as tk
from tkinter.filedialog import askdirectory
import glob
import sys # will allow us to access system specific parameters/funcs


def keeps_aletters(string): # 1 function: only keeps alphabetical letters when returning string
    aletters_word = '[]'
    for char in string:
        if char.isalpha(): # if character is in the alphabet, return alphabetical letters from parameter
            aletters_word += char
            return aletters_word.lower()



def searchFiles(): # 2 function: allows user to search for text files to run similarity test

    stopwords_txt = "Assignments\Assignment_3\StopWords.txt"
    directory = askdirectory(initialdir=stopwords_txt)

    global file_text

    data = Test_JaccardSimilarity(file_text)  # Jaccard Similarity insert
    file_text = glob.glob(directory + "/" + "*.txt") # glob glob glob glo
    tkinter_table(data)


def Test_JaccardSimilarity(files): # 3 function: WE RUN JACCARD TEST
    # we run jaccard similarity of all text files in the directoru where the user selects the specific file

    sorted_files = [] # sorted word files
    jaccardS_list = []

    for file in files:
        og_set = set_text(file)
        print(og_set)
        print()
        print()
        sorted_files.append(og_set)

    for x in sorted_files:
        checking_first = x

        for y in sorted_files:
            checking_second = y
            t_union = checking_first.union(checking_second)
            t_inter = checking_first.intersection(checking_second)
            jaccard_go = float(len(t_inter) / len(t_union)) # run simulation of the jaccard
            jaccardS_list.append(jaccard_go)

        return jaccardS_list



def set_text(textFile):  # 4 function: opens select file and creates a dictionary based on the frequency of words with a range of 25
    file = open\
        (textFile, "r", encoding="utf8")
    og_word = {}
    for line in file: # 4 function dictionary is key while our computed frequency will be the item
        line_for_words = line.split()
        for word in line_for_words:
            word = keeps_aletters(word)
            if word not in s_words:
                if word in og_word:
                    og_word[word] += 1
                else:
                    og_word[word] = 1

    dict_sorted = dict(sorted(og_word.items(), key=lambda item: item[1], reverse=True)) # take top 25 from dict
    dict_sorted_list = list\
        (dict_sorted.keys())
    new_set = set()
    for i in range(25):
        new_set.add(dict_sorted_list[i])

    return new_set



def tkinter_table(j_similarity_grid): # 5 function: tkinter data displayed. got idea from stackoverflow
    og_labell.destroy()
    og_button.destroy()

    cleantext_list = []
    for text in file_text:
        tp = text.rfind("\\")
        cleantext_list.append(text[tp + 1:])

    titl = 0
    for num in range(len(cleantext_list)):

        indexing_system = "[" + str(num) + "]"
        a = tk.Label(wdow, text=indexing_system + " " + cleantext_list[num])
        b = tk.Label(wdow, text=indexing_system)
        a.grid(row=2 + titl, column=0)
        b.grid(row=0, column=1 + titl)
        titl += 1

    for b in range(len(cleantext_list)):
            c = '%.3f' % (j_similarity_grid[b + len(cleantext_list) * num])
            d = tk.Label(wdow, text = c)
            d.grid(row=2 + b, column = 1 + num, padx = 1, pady = 1)
    description_jac = tk.Label(wdow, text = "Higher The Number Makes More Similar.")
    description_jac.grid(row=0, column = 0)
    description_jac = tk.Label(wdow, text = "Resembling Similarity To:")
    description_jac.grid(row=0, column = len(cleantext_list) + 2)
    finalbutton.grid(row=0, column = len(cleantext_list) + 3)

    for a in range(0, len(cleantext_list)):
        highest = 0
        b = None
        for b in range(0, len(cleantext_list)):
            a = a * len(cleantext_list) + b
            if highest < j_similarity_grid[a] < 1:
                b = b
                highest = j_similarity_grid[a]
        e = tk.Label(wdow, text=cleantext_list[b])
        e.grid(row=2 + a, column=len(cleantext_list) + 2, padx=1, pady=1)


file_swords = open("Assignments\Assignment_3\StopWords.txt", "r") # created for stop words only
s_words = set() # swords ching ching stop words
for word in file_swords:
    s_words.add(keeps_aletters(word))



# tkinter grid code
wdow = tk.Tk()
wdow.title("The One And Only Jaccard Similarity Test")
wdow.geometry("1200x800")

start_text = "Apply Jaccard Similarty Test on selected files\n"

og_labell = tk.Label(wdow, text = start_text)

og_button = tk.Button(wdow, text="Start", command=searchFiles)

finalbutton = tk.Button(wdow, text="Exit", command=sys.exit)

og_labell.grid(row=0, column=0)
og_button.grid(row=1, column=0)
finalbutton.grid(row=2, column=0)

wdow.mainloop()
