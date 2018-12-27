# DSA-project

#Reverse Index

import mysql.connector
import re



conn = mysql.connector.connect(user="root",
		password="1876",
		host="localhost",database = "Search_Engine2")
cursor = conn.cursor()
#def set_key(dictionary, key, value):
#	if key not in dictionary:
#		dictionary[key] = value
#	elif type(dictionary[key]) == list:
#		dictionary[key].append(value)
#	else:
		dictionary[key]=[dictionary[key],value]

def reverse_index(wordId, doc_Id):
	sqlFormula = "Insert Into Rev_Index(word_Ids, Doc_Id) Value (%s,%s)"
	doc = (wordId, doc_Id)
	cursor.execute(sqlFormula, doc)
	conn.commit()

rev_dict = dict()
cursor.execute('''Select Doc_Id,Unique_word_Id
				from forward_index ''')
myresult = cursor.fetchall()
#previous code
for row in myresult:
	doc_Id = row[0]
	#rev_dict = dict()
	#print(doc_Id)
	word_ids = repr(row[1])
	word_ids = word_ids[2:-2]
	word_ids = re.sub(r'[^a-zA-Z0-9]'," ",word_ids)
	word_ids = word_ids.split()
	#print(word_ids)
#	for ids in word_ids:
#		set_key(rev_dict,str(ids),doc_Id)
#	print(rev_dict)
#	for key,value in rev_dict.items():
#		reverse_index(int(key),str(value))
			#if doc_Id in rev_dict(str(ids):


from tkinter import *
def get():
    searchvalue=search.get()
    # search value of searchvalue variable in your files
    a=""      #store strings that you get output after searching in variable a
    result.delete(1.0,END)
    result.insert(INSERT,a)

root=Tk()
root.title("Search Engine")
topframe=Frame(root)
label=Label(text="Simple Wikipedia Search Engine")
label.pack()
search=Entry(topframe,width=60)

search.pack()
searchbutton=Button(topframe,text="Search",command=get)
searchbutton.pack()




topframe.pack(side=TOP)
bottomframe=Frame(root)
scroll=Scrollbar(bottomframe)
scroll.pack(side=RIGHT,fill=Y)
result=Text(bottomframe,width=150,height=30,yscrollcommand=scroll.set,wrap=WORD)
scroll.config(command=result.yview())
result.config(state=DISABLED)
result.pack()
bottomframe.pack()
root.mainloop()




