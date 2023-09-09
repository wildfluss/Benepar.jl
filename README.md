# Benepar.jl


Python's benepar inside Julia

## Usage

- Input 

```julia
using Spacy, Benepar, PythonCall

spacy.cli.download("en_core_web_md")

benepar.download("benepar_en3")

config = PythonCall.pydict(Dict("model"=>"benepar_en3"))

nlp = spacy.load("en_core_web_md")
nlp.add_pipe("benepar"; config=config)

text = """
    When Sebastian Thrun started working on self-driving cars at
    Google in 2007, few people outside of the company took him
    seriously. “I can tell you very senior CEOs of major American
    car companies would shake my hand and turn away because I wasn’t
    worth talking to,” said Thrun, in an interview with Recode earlier
    this week.
    """

doc = nlp(text)

for sent in doc.sents
    print("$(sent.text):")
    # for l in sent._.labels
    #     println("$(l) ")
    # end
    println("$(sent._.parse_string)")
    println()
end
```

- Output

```
When Sebastian Thrun started working on self-driving cars at
Google in 2007, few people outside of the company took him
seriously.:(S (SBAR (WHADVP (WRB When)) (S (NP (NNP Sebastian) (NNP Thrun)) (VP (VBD started) (VBG working) (PP (IN on) (NP (ADJP (NN self) (HYPH -) (VBG driving)) (NNS cars))) (PP (IN at) (NP (NNP 
) (NNP Google))) (PP (IN in) (NP (CD 2007)))))) (, ,) (NP (NP (JJ few) (NNS people)) (ADVP (IN outside) (PP (IN of) (NP (DT the) (NN company))))) (VP (VBD took) (NP (PRP him)) (ADVP (RB 
) (ADVP (RB seriously)))) (. .))

“I can tell you very senior CEOs of major American
car companies would shake my hand and turn away because I wasn’t
worth talking to,” said Thrun, in an interview with Recode earlier
this week.
:(SINV (`` “) (S (NP (PRP I)) (VP (MD can) (VP (VB tell) (NP (PRP you)) (SBAR (S (NP (NP (ADJP (RB very) (JJ senior)) (NNS CEOs)) (PP (IN of) (NP (JJ major) (JJ American) (NN 
) (NN car) (NNS companies)))) (VP (MD would) (VP (VP (VB shake) (NP (PRP$ my) (NN hand))) (CC and) (VP (VP (VB turn) (ADVP (RB away))) (SBAR (IN because) (S (NP (PRP I)) (VP (VBD was) (RB n’t) (ADJP (JJ 
) (S (ADJP (JJ worth) (S (VP (VBG talking) (PP (IN to)))))))))))))))))) (, ,) ('' ”) (VP (VBD said)) (NP (NNP Thrun)) (, ,) (PP (IN in) (NP (NP (DT an) (NN interview)) (PP (IN with) (NP (NNP Recode))))) (NP (ADVP (RBR earlier)) (DT 
) (DT this) (NN week)) (. .) (. 
))
```
