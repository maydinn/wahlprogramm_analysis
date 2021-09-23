# wahlprogram_analysis


DESCRIPTION:

In this repository, you will find the content analysis of parties' “Wahlprogramm” in Germany.

DATA:

https://www.bundestagswahl-2021.de/wahlprogramme/

examples of some important used methods:
	# cleaning text data from punctions and stop worlds and similar words 
	def clean_text(doc):    
	    text_tokens = nlp(doc)
	    tokens_without_punc = [token.text for token in text_tokens if token.text.isalpha()]
	    tokens_without_sw = [t for t in tokens_without_punc if t.lower() not in stop_words]
	    doc = nlp(" ".join(tokens_without_sw ))
	    text_cleaned=[i.lemma_ for i in doc]
	    return " ".join(text_cleaned)

	# dividing text into sentences
	def get_sent(x):
	    l = []
	    for i in x.split('.'):
	        if i != '':
	            l.append(i)
	    return l

Some insights:

The following five words set for each party get a high score from TdfVectoricer. 

CDU : deutschland, land, starken, europa, setzen
SPD : europa, unterstützen, deutschland, zukunft, arbeit
Green : mensch, stärken, brauchen, deutschland, setzen

And then, I applied a word embedding method to analyze similarities between words. I used Word2Vec from the gensim library. For instance: 
the most 5 similar words to 
“Digitalisierung” in parties' “Wahlprogramm” are following:
for CDU:
'Gebäude', 'Startups', 'Lebensqualität', 'Klimawandel', 'zugänglich'

for SDP: 
'erarbeiten', ’Rahmenbedingungen', 'Wert', 'modernisieren', 'Verein'

for Green:
 'Sicherheitspolitik',’Produkt',’funktionierend', 'Transformation',’Verwaltung'

Moreover, since each word is represented by a vector in word embedding, it allows making word prediction by defining words as either negative or positive. For instance, after defining Deutschland, Digitalisierung positive. We have 'Aufbruch' for CDU, 'Wert' for SDP, 'Sicherheitspolitik' for Green.

Although there are several sections for each party program, I tried to make three clusters by using the negative vectorize method and want to show the top 15 words for the party regarding their clusters. 

For CDU;

THE TOP 15 WORDS FOR TOPIC #0
'digitale', 'fördern', 'sicherheit', 'bund', 'unternehmen', 'setzen', 'bürger', 'stark', 'mensch', 'stärken', 'digital', 'staat', 'deutschland', 'schaffen', 'land'


THE TOP 15 WORDS FOR TOPIC #1
'stark', 'setzen', 'eng', 'partner', 'demokratie', 'welt', 'sicherheit', 'deutschland', 'global', 'eu', 'union', 'gemeinsam', 'europäisch', 'europäische', 'europa'


THE TOP 15 WORDS FOR TOPIC #2
'mensch', 'aufstieg', 'sozial', 'jugendliche', 'fördern', 'beruf', 'mann', 'euro', 'gewalt', 'eltern', 'schule', 'frau', 'bildung', 'familie', 'kind'

For SPD;

THE TOP 15 WORDS FOR TOPIC #0
'rente', 'ausbildung', 'behinderung', 'eltern', 'alt', 'frau', 'junge', 'respekt', 'leben', 'gesellschaft', 'familie', 'arbeit', 'jugendliche', 'mensch', 'kind'


THE TOP 15 WORDS FOR TOPIC #1
'russland', 'respekt', 'global', 'stärken', 'krise', 'setzen', 'gemeinsam', 'welt', 'leben', 'zukunft', 'demokratie', 'europäisch', 'eu', 'europäische', 'europa'


THE TOP 15 WORDS FOR TOPIC #2
'erhalten', 'sichern', 'nachhaltig', 'wichtig', 'energie', 'kommune', 'entwicklung', 'ziel', 'digitale', 'brauchen', 'sorgen', 'deutschland', 'fördern', 'unterstützen', 'digital'



For Green Party;

THE TOP 15 WORDS FOR TOPIC #0
'zusammenarbeit', 'deutschland', 'sicherheit', 'demokratie', 'menschenrechte', 'stärken', 'setzen', 'international', 'gemeinsam', 'europäische', 'staat', 'europa', 'global', 'eu', 'europäisch'


THE TOP 15 WORDS FOR TOPIC #1
'kitas', 'stärken', 'jugendhilfe', 'frau', 'leben', 'ausbildung', 'lernen', 'eltern', 'brauchen', 'familie', 'mensch', 'bildung', 'schule', 'jugendliche', 'kind'


THE TOP 15 WORDS FOR TOPIC #2
'ermöglichen', 'kommune', 'leben', 'unterstützen', 'ökologisch', 'brauchen', 'co', 'stärken', 'fördern', 'mensch', 'nachhaltig', 'land', 'unternehmen', 'schaffen', 'öffentlich'


