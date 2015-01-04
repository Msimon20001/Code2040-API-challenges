Code2040-API-challenges
=======================
import urllib

import requests

import json

import datetime

import time

def registration():
""" Code to register on Code2040"""

    body = {'email': 'msimon20001@gmail.com', 'github':'https://github.com/Msimon20001/Code2040-API-challenges'}
    jsonarray = json.dumps(body)
    response = requests.post("http://challenge.code2040.org/api/register",data=jsonarray)
    r = response.text
    toke = json.loads(response.text)
    return r 
    
token = {"result":"jRTFqUHNIV"} # manually copied and pasted the print of response.text

toke2 = registration()          # did not know about json.loads at the time 


def getinfo(http):
    """ returns value from Api as data type input the http into a ... my automatic poster"""
    
    body = {'token': token['result']}
    
    jsonarray = json.dumps(body)
    
    resp = requests.post(http,data=jsonarray)
    
    basestring = resp.text
    
    usestring = json.loads(resp.text)
    
    return usestring
    
    
def sendinfo(fromhttp,tohttp,func,key1):
 """takes a from adress a to adress and a function and it sends the result of function to the to adress"""
 
    use = getinfo(fromhttp)['result']                            # gives the needed value for API
    
    replace = func(use)                                          # does whatever function on that value
    
    newd = {'token':token['result'], key1:replace}               # makes new dictionary with token:answer
    
    jsonarray = json.dumps(newd)                                 # jsonifys new dictionary
    
    resp = requests.post(tohttp, data=jsonarray)                 # sends out new json dict to http
    
    bases = resp.text                                            # theses last two lines merely check if there is an error 
    
    usestring = json.loads(bases)             
    
    return use ,newd , jsonarray , bases , usestring

def needlehay(fromhttp,tohttp,func,key1,key2,key3):
    """sendinfo specifically for needle in haystack or atleast for 2 part dictionarys"""
    
                                                                       # key1 is the key of the answer the problem asks to be sent 
                                                                       
    use = getinfo(fromhttp)['result']                                  # gives the needed value for API
    
    use2 = use[key2]                                                   # key2 is first dict key in inner dictionary
    
    use3 = use[key3]                                                   # key3 is second dict key in inner dictionary
    
    replace = func(use2,use3)                                          # does whatever function on that value
    
    newd = {'token':token['result'], key1:replace}                     # makes new dictionary with token:answer
    
    jsonarray = json.dumps(newd)                                       # jsonifys new dictionary
    
    resp = requests.post(tohttp, data=jsonarray)                       # sends out new json dict to http
    
    bases = resp.text                                                  # theses last two lines merely check if there is an error 
    
    usestring = json.loads(bases)                               
    
    return use ,newd , jsonarray , bases , usestring                  # returns different stages of post request

def reversestring(s):
    """returns a reversed string specifically for Code2040 Api challenge uses recursion, to submit answer i used code : sendinfo(getstringendpoint,validateendpoint,reversestring)"""
   
    if s == '':
        return ''
   
    else:
        return reversestring(s[1:]) + s[0]
def findword(w,L):
    """finds index of word in list recursion can be similarly done in java"""
   
    if L[0]==w:
        return 0
   
    else:
        return 1 + findword(w,L[1:])
    
def prefixcheck(pre,word):
    """checks if word contains prefix"""
   
    a = len(pre)
   
    if pre == word[0:a]:
        return False
   
    else:
        return True
    
def prefix(Word,List):
    """takes out everything in list L that has prefix Word"""
    
    PrefixList = filter(lambda x: prefixcheck(Word,x),List)     # Lamda is temporary function, basically it takes every value of the list and checks if the word has the prefix in it, if it does prefix check returns false and filter does not accept if not prefixcheck returns true and filter builds list
    
    TrueList = list(PrefixList)                                 # learned: filter doesnt pass a real list, so convert to list
                                                                
    return TrueList

def prefixOther(Word,List):
    """ alternate to prefix using recursion"""
    
    if List == []:
        return[]
    
    elif  word == L[0][0,len(word)]:
        return prefixOther(Word,List[1:])
    
    else:
        return [L[0]]+ prefix(Word,List[1:])

def DeltaTime(Date,Sec):
    """finds the new date with a given number of seconds"""
    # my Delta time program is coming scarily close except the hours are always off by exactly 2

    Date1= iso8601.parse_date(Date)           # parses is860 format to datetime format 

    Time1= int(time.mktime(Date1.timetuple())) # finds seconds that have passed since 1900 for date given

    Time2= float(Time1 + Sec) # adds interval seconds to that time 

    Date3= datetime.datetime.fromtimestamp(Time2) # finds new date time from data

    return Date3.strftime('%Y-%m-%dT%H:%M:%S.000Z') #represents new date as iso8601

Code2040 API challenges
