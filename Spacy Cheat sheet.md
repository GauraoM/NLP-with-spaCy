#### load the installed model
nlp = spacy.load("en_core_web_sm") --- This is small model
nlp = spacy.load("en_core_web_md") --- This is medium model

#### Processing text
processing text with nlp object returns a Doc object that holds all the information about tokens.

doc = nlp(text)

#### the left most token and right most token
Gives left most token of the given token

token2.left_edge
token2.right_edge

#### lemetization
Root word of the sentence.
token2.lemma_

#### Morphological operations
Gives what type of word it is
token2.morph

#### POS tag
Gives whether it is Noun, Proper noun, Verb etc.

token2.pos_

#### Dependency label
Gives relation between token 
token2.dep_

#### Label
Gives the label which the entity belongs to
ent.label_

#### displacy
Shows how the sentence is structured.

displacy.render(doc, style="dep", jupyter = True)

displacy.render(doc, style="ent", jupyter = True)

#### mapping-word-vector-to-the-most-similar-closest-word-using-spacy
your_word = "country"

ms = nlp.vocab.vectors.most_similar(np.asarray([nlp.vocab.vectors[nlp.vocab.strings[your_word]]]), n=10)
words = [nlp.vocab.strings[w] for w in ms[0][0]]

#### Doc similarity
Find similarity between two documents.

doc1.similarity(doc2)

#### Analyze pipes
Gives insight about pipelines

nlp.analyze_pipes()

#### entity ruler
If the label is incorrectly classified then add a pattern to the pipeline

nlp = spacy.load("en_core_web_sm")

ruler = nlp2.add_pipe("entity_ruler",before="ner")

patterns = [
    {"label":"GPE", "pattern":"West Chestertenfieldville"}

]

ruler.add_patterns(patterns)

#### Matcher
Like here in add "EMAIL_ADDRESS" as vocab 

matcher = Matcher(nlp.vocab)

pattern = [{"LIKE_EMAIL":True}]

matcher.add("EMAIL_ADDRESS",[pattern])

#### Adding multiple things to token
Op - here op is Operator to determine how often to match a token pattern
pos: VERB - the next thing to be occured to PROPN is a verb
greedy - longest sequence

matcher = Matcher(nlp.vocab)
pattern = [{"POS": "PROPN", "OP": "+"},{"POS":"VERB"}]
matcher.add("PROPER_NOUNS", [pattern], greedy='LONGEST')
doc = nlp(text)
matches = matcher(doc)
print (len(matches))
# Sort with start of token
matches.sort(key = lambda x: x[1])
for match in matches[:10]:
    print (match, doc[match[1]:match[2]])

#### Reading JSON
with open("alice.json", "r") as f:
    data = json.load(f)

#### Save to disk
nlp.to_disk("spacy/new_en_cor_web_sm)

#### regex Find pattern
To get the particular output based on pattern

pattern = r"Paul [A-Z]\w+"

matches = re.finditer(pattern, text)

#### CReate a temporary span
Grab the start and end from each match.Create a temporary span that will be equal to where the characters start and end in the doc object.

start, end = match.span()
span = doc.char_span(start, end)


