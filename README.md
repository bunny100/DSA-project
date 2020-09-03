# Local Search Engine

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


#Clearing the text body:
def	filteredwords(text): 
	global doc_words
	b=["a's",',','_',"-","In", 'able','a','b','c','d','e','f','g','h','i','j','k','l','m','n',
	'p','q','r','s','t','u','v','w','x','y','z',"'", 'about', 'above', 'according', 'accordingly', 
	'across','s', 'actually', 'after', 'afterwards', 'again', 'against', 'search','links',
	"ain't", 'all', 'allow', 'allows', 'almost', 'alone', 'along','wikipedia', 'already', 
	'also', 'although', 'always', 'am', 'among', 'amongst', 'an', 'and', 'another', 
	'any', 'anybody', 'anyhow', 'anyone', 'anything', 'anyway', 'anyways', 'anywhere', 
	'apart', 'appear', 'appreciate', 'appropriate', 'are', "aren't", 'around', 
	'as', 'aside', 'ask', 'asking', 'associated', 'at', 'available', 'away', 'views',
	'awfully', 'be', 'became', 'because', 'become', 'becomes', 'becoming', 'been', 
	'before', 'beforehand', 'behind', 'being', 'believe', 'below', 'beside', 
	'besides', 'best', 'better', 'between', 'beyond', 'both', 'brief', 'but', 'by', 
	"c'mon", "c's", 'came', 'can', "can't", 'cannot', 'cant', 'cause', 'causes', 
	'certain', 'certainly', 'changes', 'clearly', 'co', 'com', 'come', 'comes', 
	'concerning', 'consequently', 'consider', 'considering', 'contain', 
	'containing', 'contains', 'corresponding', 'could', "couldn't", 'course', 
	'currently', 'definitely', 'described', 'despite', 'did', "didn't", 'different', 
	'do', 'does', "doesn't", 'doing', "don't", 'done', 'down', 'downwards', 
	'during', 'each', 'edu', 'eg', 'eight', 'either', 'else', 'elsewhere', 'enough', 
	'entirely', 'especially', 'et', 'etc', 'even', 'ever', 'every', 'everybody', 'everyone', 
	'everything', 'everywhere', 'ex', 'exactly', 'example', 'except', 'far', 'few', 
	'fifth', 'first', 'five', 'followed', 'following', 'follows', 'for', 
	'former', 'formerly', 'forth', 'four', 'from', 'further', 'furthermore', 
	'get', 'gets', 'getting', 'given', 'gives', 'go', 'goes', 'going', 
	'gone', 'got', 'gotten', 'greetings', 'had', "hadn't", 'happens', 
	'hardly', 'has', "hasn't", 'have', "haven't", 'having', 'he', "he's", 
	'hello', 'help', 'hence', 'her', 'here', "here's", 'hereafter', 
	'hereby', 'herein', 'hereupon', 'hers', 'herself', 'hi', 'him', 
	'himself', 'his', 'hither', 'hopefully', 'how', 'howbeit', 'however', 
	"i'd", "i'll", "i'm", "i've", 'ie', 'if', 'ignored', 'immediate',
	'in', 'inasmuch', 'inc', 'indeed', 'indicate', 'indicated',
	'indicates', 'inner', 'insofar', 'instead', 'into', 'inward', 
	'is', "isn't", 'it', "it'd", "it'll", "it's", 'its', 'itself', 
	'just', 'keep', 'keeps', 'kept', 'know', 'knows', 'known', 'last', 
	'lately', 'later', 'latter', 'latterly', 'least', 'less', 'lest', 
	'let', "let's", 'like', 'liked', 'likely', 'little', 'look', 
	'looking', 'looks', 'ltd', 'mainly', 'many', 'may', 'maybe', 
	'me', 'mean', 'meanwhile', 'merely', 'might', 'more', 'moreover', 
	'most', 'mostly', 'much', 'must', 'my', 'myself', 'name', 'namely', 
	'nd', 'near', 'nearly', 'necessary', 'need', 'needs', 'neither', 
	'never', 'nevertheless', 'new', 'next', 'nine', 'no', 'nobody', 'non', 'none', 
	'noone', 'nor', 'normally', 'not', 'nothing', 'novel', 'now', 
	'nowhere', 'obviously', 'of', 'off', 'often', 'oh', 'ok', 'okay', 'old', 
	'on', 'once', 'one', 'ones', 'only', 'onto', 'or', 'other', 'others', 
	'otherwise', 'ought', 'our', 'ours', 'ourselves', 'out', 'outside', 
	'over', 'overall', 'own', 'particular', 'particularly', 'per', 
	'perhaps', 'placed', 'please', 'plus', 'possible', 'presumably', 
	'probably', 'provides', 'que', 'quite', 'qv', 'rather', 'rd', 're', 'really', 
	'reasonably', 'regarding', 'regardless', 'regards', 'relatively', 'respectively', 
	'right', 'said', 'same', 'saw', 'say', 'saying', 'says', 'second', 
	'secondly', 'see', 'seeing', 'seem', 'seemed', 'seeming', 'seems', 
	'seen', 'self', 'selves', 'sensible', 'sent', 'serious', 'seriously', 
	'seven', 'several', 'shall', 'she', 'should', "shouldn't", 'since', 'six', 'so', 
	'some', 'somebody', 'somehow', 'someone', 'something', 'sometime', 'sometimes', 
	'somewhat', 'somewhere', 'soon', 'sorry', 'specified', 'specify', 'specifying', 
	'still', 'sub', 'such', 'sup', 'sure', "t's", 'take', 'taken', 'tell', 'tends', 
	'th', 'than', 'thank', 'thanks', 'thanx', 'that', "that's", 'thats', 
	'the', 'their', 'theirs', 'them', 'themselves', 'then', 'thence', 'there', 
	"there's", 'thereafter', 'thereby', 'therefore', 'therein', 'theres', 
	'thereupon', 'these', 'they', "they'd", "they'll", "they're", 
	"they've", 'think', 'third', 'this', 'thorough', 'thoroughly', 'those', 
	'though', 'three', 'through', 'throughout', 'thru', 'thus', 'to', 
	'together', 'too', 'took', 'toward', 'towards', 'tried', 
	'tries', 'truly', 'try', 'trying', 'twice', 'two', 'un',
	'under', 'unfortunately', 'unless', 'unlikely', 'until', 'unto', 'up', 'upon', 
	'us', 'use', 'used', 'useful', 'uses', 'using', 'usually', 'value', 'various', 
	'very', 'via', 'viz', 'vs', 'want', 'wants', 'was', "wasn't", 'way', 'we', "we'd", "we'll", 
	"we're", "we've", 'welcome', 'well', 'went', 'were', "weren't", 'what', 
	"what's", 'whatever', 'when', 'whence', 'whenever', 'where', "where's", 'whereafter', 
	'whereas', 'whereby', 'wherein', 'whereupon', 'wherever', 'whether', 
	'which', 'while', 'whither', 'who', "who's", 'whoever', 
	'whole', 'whom', 'whose', 'why', 'will', 'willing', 'wish', 
	'with', 'within', 'without', "won't", 'wonder', 'would', 'would', 
	"wouldn't", 'yes', 'yet', 'you', "you'd", "you'll", 
	"you're", "you've", 'your', 'yours', 'yourself', 'yourselves', 'zero']


	#if (text in b or text in doc_words):
	if (text in b):
		return False
	else:
		if (text not in distinct_words):
			distinct_words.append(text)
			if len(text) >1000:
				text=text[1:50]
			Unique_words([text])	
		doc_words.append(text)

		return True

