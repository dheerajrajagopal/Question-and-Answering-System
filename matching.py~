#! /usr/bin/env python

import nltk
import string
import question_analysis
import preprocessing
import MicrosoftNgram
import itertools
from nltk.corpus import stopwords

#from nltk.corpus import wordnet as wn


list_tuples = preprocessing.actual_tuples

list_tuples.sort()

keywords = question_analysis.keywords_analysis 

tuples_needed = []

concept = []
for i in range(len(keywords)):
	for j in range(len(list_tuples)):
		if( list_tuples[j].startswith(keywords[i]+",")):
			tuples_needed.append(list_tuples[j])

#print tuples_needed

concept2 = []

for i in range(len(tuples_needed)):
	a = tuples_needed[i].split(",")
	b = nltk.word_tokenize(a[1])
	
	for j in range(len(b)):
		concept2.append(b[j])



tuples_normalized = []
	
s = MicrosoftNgram.LookupService()

string_perm = itertools.permutations(keywords)

string = []

for i in string_perm:
	string.append(" ".join(i))


results = []

for i in range(len(string)):
	for t in s.Generate(string[i], maxgen=40): results.append(t)

answers = []

for i in range(len(results)):
	 answers.append(results[i][0])

concept2 = list(set(concept2))

list_answers =  list( (set(concept2) & set(answers) ) - set(keywords) )

if (len(list_answers) == 0):
	list_answers = answers

list_answers1 = []

for i in range(len(list_answers)):
	tagged = nltk.pos_tag(nltk.word_tokenize(list_answers[i]))
	#print tagged
	if( tagged[0][1].startswith("N") or tagged[0][1].startswith("V") or tagged[0][1].startswith("J") ):
		if( list_answers[i] not in stopwords.words('english') and list_answers[i].isdigit() == False):
			list_answers1.append(list_answers[i])



print "the most probable answers for your question"
print list_answers1 

	


