from __future__ import division
from collections import defaultdict
from math import log
tags=['science', 'style', 'culture', 'life', 'economics', 'business', 'travel',
          'forces', 'media', 'sport'];
def train():
    file=open('news_train.txt');

    classes = defaultdict(lambda:0);
    w_freq = defaultdict(lambda:0);
    w_class=defaultdict(lambda:0);
    count=0;
    k=0;
    str_quan=0;
    for line in file:
        str_quan+=1;
        count=0;
        k=0;
        data = line.split();
        classes[data[0]] += 1;
        for letters in line:
            if(letters=='\t'):
                count+=1;
            if(count==2):
                line=line[k:];
                break;

        words=line.split();
        for word in words:
            if((word[len(word)-1]=='.')or(word[len(word)-1]==',')):
                word=word[:len(word)-1];
            w_freq[data[0], word] += 1;
            w_class[data[0]]+=1;



    for tag, word in w_freq:
        (w_freq[tag, word]) =log(((w_freq[tag, word]))/(w_class[tag]),10**(-7));
    for f in classes:
        classes[f] =log(classes[f]/str_quan,10**(-7));

    return classes, w_freq,w_class;

test=open('news_test.txt');
count = 0;
k = 0;
classes,w_freq,w_class=train();
file=open('news_output','w');
for line in test:
    probability = defaultdict(lambda: 1);

    count = 0;
    k = 0;
    for letters in line:
        if (letters == '\t'):
            count += 1;
        if (count == 1):
            line = line[k:];
            break;

    words = line.split();
    for word in words:
        if ((word[len(word) - 1] == '.')or  (word[len(word) - 1] == ',')):
            word = word[:len(word) - 1];
        for tag in tags:
           if(w_freq[tag,word]==0):
               w_freq[tag,word]=1/(2*w_class[tag]);
           probability[tag]*=w_freq[tag,word];


    for tag in tags:
        probability[tag]*=classes[tag];
    max=probability['sport'];

    cl='sport';
    for tag in tags:

        if (probability[tag]>max):
            max=probability[tag];
            cl=tag;


    file.write(cl+'\n');




