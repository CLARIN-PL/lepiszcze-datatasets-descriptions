# Dialogue Acts - DiaBiz.Kom

## Description

It consists of 1,277,962 tokens in 1,104 transcribed call center phone conversations spanning eight domains. Each example is annotated by three linguists (in a 2+1 system, with an inter-annotator agreement of 0.78 for annotation borders and categories and 0.86 for annotation borders) with dialogue acts in compliance with ISO 64217-2:2012 standard with a layer of information concerning communicative functions. Within the benchmark, we consider the task of dialogue act classification, where each utterance is provided with its role in the dialogue. Sample and a detailed description can be obtained from [the official site](https://clarin-pl.eu/dspace/handle/11321/886) as well as the corresponding [recordings](https://clarin-pl.eu/dspace/handle/11321/887). DiaBiz.Kom is annotation layer on top of DiaBiz - corpus  of polish call center dialogs.

## Tasks (input, output and metrics)

**Input** ('text*'* column): fragment of a dialogue with a call center employee

**Output** ('*name'* column): class of interaction (one of the 54 possible classes)

**Domains**: several key business domains: banking, debt, energy, insurance, medicine, rental, telcom, tourism

**Measurements**: F1-Score

**Example***:* 

*“Proszę o to, aby przygotował pan sobie od ośmiu do dwudziestu cyfr. Przełączę pana do automatycznej części serwisu. Proszę, aby wpisał pan tam cyfry na klawiaturze telefonu i następnie zatwierdził to (yy) taką kratką na klawiaturze. Następnie proszę na stronie logowania podać (yy) swój numer klienta, ten, który pan mi podał, (yy) no i to hasło, które pan sobie ustali (yy) teraz w tej części automatycznej. (yy) To hasło nie będzie działało na stałe. (yy) Po prostu (yy) po zalogowaniu na te dane, które pan teraz ustalił, ustali pan sobie takie już hasło docelowe.”* → **instruct**

## Data splits

```
| Subset     |   Cardinality |
|:-----------|--------------:|
| train      |         70454 |
| validation |          8807 |
| test       |          8807 |
```

## Class distribution

```
| Class                  |   train |   validation |    test |
|:-----------------------|--------:|-------------:|--------:|
| stalling               | 0.22317 |      0.22323 | 0.22312 |
| inform                 | 0.16466 |      0.16464 | 0.16464 |
| interactionStructuring | 0.10984 |      0.10991 | 0.10980 |
| autoPositive           | 0.08740 |      0.08732 | 0.08743 |
| answer                 | 0.06949 |      0.06949 | 0.06949 |
| selfCorrection         | 0.02816 |      0.02816 | 0.02816 |
| setQuestion            | 0.02800 |      0.02793 | 0.02805 |
| propositionalQuestion  | 0.02710 |      0.02702 | 0.02714 |
| thanking               | 0.02559 |      0.02566 | 0.02555 |
| contactIndication      | 0.02456 |      0.02453 | 0.02453 |
| fragment               | 0.02113 |      0.02112 | 0.02112 |
| checkQuestion          | 0.01537 |      0.01544 | 0.01533 |
| request                | 0.01198 |      0.01204 | 0.01192 |
| confirm                | 0.01195 |      0.01192 | 0.01204 |
| testQuestion           | 0.01126 |      0.01124 | 0.01124 |
| SelfCompletion         | 0.01033 |      0.01033 | 0.01033 |
| returnGoodbye          | 0.01009 |      0.01011 | 0.01011 |
| initSelfIntroduction   | 0.00911 |      0.00908 | 0.00908 |
| initGoodbye            | 0.00908 |      0.00908 | 0.00908 |
| initGreeting           | 0.00896 |      0.00897 | 0.00897 |
| opening                | 0.00860 |      0.00863 | 0.00863 |
| instruct               | 0.00825 |      0.00818 | 0.00829 |
| suggest                | 0.00805 |      0.00806 | 0.00806 |
| returnGreeting         | 0.00749 |      0.00749 | 0.00749 |
| agreement              | 0.00636 |      0.00636 | 0.00636 |
| choiceQuestion         | 0.00563 |      0.00556 | 0.00568 |
| offer                  | 0.00538 |      0.00534 | 0.00545 |
| other                  | 0.00481 |      0.00488 | 0.00477 |
| acceptRequest          | 0.00470 |      0.00466 | 0.00477 |
| pausing                | 0.00343 |      0.00352 | 0.00341 |
| alloPositive           | 0.00336 |      0.00329 | 0.00341 |
| promise                | 0.00319 |      0.00318 | 0.00318 |
| returnSelfIntroduction | 0.00288 |      0.00295 | 0.00284 |
| selfError              | 0.00287 |      0.00284 | 0.00295 |
| feedbackElicitation    | 0.00277 |      0.00284 | 0.00273 |
| acceptOffer            | 0.00270 |      0.00273 | 0.00261 |
| apology                | 0.00217 |      0.00216 | 0.00216 |
| acceptSuggest          | 0.00145 |      0.00148 | 0.00148 |
| sympathyExpression     | 0.00142 |      0.00136 | 0.00148 |
| retraction             | 0.00111 |      0.00114 | 0.00114 |
| otherQuestion          | 0.00099 |      0.00102 | 0.00091 |
| contactCheck           | 0.00089 |      0.00091 | 0.00091 |
| disagreement           | 0.00065 |      0.00068 | 0.00068 |
| declineOffer           | 0.00064 |      0.00068 | 0.00057 |
| autoNegative           | 0.00057 |      0.00057 | 0.00057 |
| disconfirm             | 0.00043 |      0.00045 | 0.00045 |
| declineSuggest         | 0.00034 |      0.00034 | 0.00034 |
| recording              | 0.00034 |      0.00034 | 0.00034 |
| acceptThanking         | 0.00031 |      0.00034 | 0.00023 |
| declineRequest         | 0.00024 |      0.00023 | 0.00023 |
| acceptApology          | 0.00024 |      0.00023 | 0.00023 |
| completion             | 0.00017 |      0.00011 | 0.00023 |
| ThirdParty             | 0.00017 |      0.00011 | 0.00023 |
| addressRequest         | 0.00014 |      0.00011 | 0.00011 |
```

## Citation

DiaBiz.Kom sample:

```
@misc{11321/886,	
 title = {{DiaBiz}.Kom sample 1.0},	
 author = {Oleksy, Marcin and Wieczorek, Jan and Domoga{\l}a, Aleksandra and Dru{\.z}y{\l}owska, Dorota and Klyus, Julia and Wr{\'o}{\.z}, Anita and Miko{\'s}, Daria and Hwaszcz, Krzysztof and Kędzierska, Hanna},	
 url = {http://hdl.handle.net/11321/886},	
 note = {{CLARIN}-{PL} digital repository},	
 copyright = {Creative Commons - Attribution-{NonCommercial}-{NoDerivatives} 4.0 International ({CC} {BY}-{NC}-{ND} 4.0)},	
 year = {2022}	
}
```

## License

The dataset is not public. However you can use sample under the following license.

```
Creative Commons - Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)
```

## Links

[Sample](https://clarin-pl.eu/dspace/handle/11321/886)

[Recordings](https://clarin-pl.eu/dspace/handle/11321/887)