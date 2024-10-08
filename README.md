```json
{
  "Content": {
    "Version": "2019-10-30",
    "StartAction": "1ff34355-4c6a-42fb-8e71-627d4ffcde6a",
    "Metadata": {
      "entryPointPosition": {
        "x": 106.4,
        "y": -152
      },
      "ActionMetadata": {
        "1ff34355-4c6a-42fb-8e71-627d4ffcde6a": {
          "position": {
            "x": 148.8,
            "y": -5.6
          }
        },
        "a403434c-d7b9-4cd6-80c3-ce76d77112ea": {
          "position": {
            "x": 155.2,
            "y": 196
          }
        },
        "fbd09b5a-c04e-46c9-900f-3bcbfb693913": {
          "position": {
            "x": 792.8,
            "y": 116
          }
        },
        "053786fc-1a9d-49bb-9f3b-0615313e7475": {
          "position": {
            "x": 770.4,
            "y": -327.2
          },
          "parameters": {
            "LambdaFunctionARN": {
              "displayName": "Voice-to-chat-transfer"
            }
          },
          "dynamicMetadata": {
            "check": false
          }
        },
        "c3d3116b-4833-414d-85c7-54d7ba28ce0a": {
          "position": {
            "x": 1349.6,
            "y": 49.6
          }
        },
        "a4893b51-4ae1-44ba-8127-0ad84b24d220": {
          "position": {
            "x": 1794.4,
            "y": -236
          }
        },
        "51925f2b-42d6-4172-8dcc-c794be502eff": {
          "position": {
            "x": 1104,
            "y": -358.4
          }
        },
        "3b2ac413-3ab7-4702-8545-8d4e416da148": {
          "position": {
            "x": 389.6,
            "y": -86.4
          },
          "conditionMetadata": [
            {
              "id": "b9640d13-b5f7-4b26-9d52-65535f8da614",
              "value": "1"
            },
            {
              "id": "46126ec3-e051-484e-9a0f-9aeba2dd982f",
              "value": "2"
            }
          ]
        },
        "4750120e-10b0-4cd8-92af-664d52233b80": {
          "position": {
            "x": 1095.2,
            "y": 191.2
          }
        },
        "24d5690d-cdfc-4e17-a84f-d018629c7cf8": {
          "position": {
            "x": 1095.2,
            "y": -102.4
          }
        },
        "3de54805-ed88-465a-b9d7-ced52cd08303": {
          "position": {
            "x": 791.2,
            "y": -136
          },
          "parameters": {
            "LambdaFunctionARN": {
              "displayName": "Voice-to-chat-transfer"
            }
          },
          "dynamicMetadata": {
            "check": false
          }
        }
      },
      "Annotations": [],
      "name": "voice to chat Module",
      "description":"Sagar: Invoked from Main IVR to enable functionality to deflect Voice Call to Chat Channel",
      "status":"published",
      "hash":[]
    },
    "Actions":[
      {
        "Parameters":{
          "FlowLoggingBehavior":"Enabled"
        },
        "Identifier":"1ff34355-4c6a-42fb-8e71-627d4ffcde6a",
        "Type":"UpdateFlowLoggingBehavior",
        "Transitions":{
          “NextAction”:“a403434c-d7b9–4cd6–80c3–ce76d77112ea”
        }
      },
      {
        “Parameters”:{
           “RecordingBehavior”:{
             “RecordedParticipants”:[“Agent”,“Customer”]
           },
           “AnalyticsBehavior”:{
             “Enabled”:“True”,
             “AnalyticsLanguage”:“en-US”,
             “AnalyticsRedactionBehavior”:“Disabled”,
             “AnalyticsRedactionResults”:“RedactedAndOriginal”,
             “ChannelConfiguration”:{
               “Chat”:{
                 “AnalyticsModes”:[]
               },
               “Voice”:{
                 “AnalyticsModes”:[“PostContact”]
               }
             }
           }},
           “Identifier”:“a403434c-d7b9–4cd6–80c3–ce76d77112ea”,
           “Type”:“UpdateContactRecordingBehavior”,
           “Transitions”:{
             “NextAction”:“3b2ac413-d3ab7–4702–8545–8d4e416da148”
           }
         },
         { 
           “Parameters”: { 
             “Text”:“error”
           }, 
           “Identifier”:“fbd09b5a-c04e–46c9–900f–3bcbfb693913”, 
           “Type”:“MessageParticipant”, 
           “Transitions”: { 
             “NextAction”:“4750120e–10b0–4cd8–92af–664d52233b80”, 
             “Errors”: [ 
               { 
                 “NextAction”:“4750120e–10b0–4cd8–92af–664d52233b80”, 
                 “ErrorType”:“NoMatchingError”
               } 
             ] 
           } 
         }, 
         { 
           “Parameters”: { 
             “LambdaFunctionARN”:“arn:aws:lambda:us-east:768637739934:function:Voice-to-chat-transfer”, 
             “InvocationTimeLimitSeconds”:“3”, 
             “LambdaInvocationAttributes”: { 
               “check”:“email”
             }, 
             “ResponseValidation”: { 
               “ResponseType”:“STRING_MAP”
             } 
           }, 
           “Identifier”:“053786fc -1 a9 d -49 bb -9 f 3 b -0615313 e 7475”, 
           “Type”:“InvokeLambdaFunction”, 
           “Transitions”: { 
             “NextAction”:“51925 f2 b -42 d 6 -4172 -8 dcc-c794be502eff”, 
             “Errors”: [ 
               { 
                 “NextAction”:“ a4893 b51 - 4 ae1 - 44 ba - 8127 - 0 ad84 b24 d220”, 
                 “ErrorType”:“NoMatchingError”
               } 
             ] 
           } 
         },  
         {  
           “Parameters”：{  
              “Text”：{  
                ”You will receive a chat bot link for the chat channel to your registered Email. Please attempt to click the link so that you can use the chatbot.\nThank you for calling have a nice day.”  
              },  
              ”Identifier”：{  
                ”51925 f2 b -42 d 6 -4172 -8 dcc-c794be502eff”，  
                ”Type”：{  
                   ”MessageParticipant”，  
                   ”Transitions”：{  
                      ”NextAction”：{  
                         ”a4893 b51 - 4 ae1 - 44 ba - 8127 - 0 ad84 b24 d220”，  
                         ”Errors”：{  
                            ”NextAction”：{  
                               ”c3 d3116 b --4833 --414d --85 c7 --54 d7 ba28 ce0 a”，  
                               ”ErrorType”：{  
                                  ”NoMatchingError”  
                               }  
                            }  
                         }  
                      }  
                   }   
                }   
              },   
              ”Parameters”：{   
                ”Text”：{   
                  ”You can choose to receive Email Or SMS Texts please select your preference to send the Chat Link to an Email please Press 1 and to send it to a Mobile device Press 2.”,   
                  ”StoreInput”：false,   
                  ”InputTimeLimitSeconds”：5   
                },   
                ”Identifier”：{   
                  ”3b2ac413-d7b9--4702--8545--8d4e416da148”，   
                  ”Type”：{   
                     ”GetParticipantInput”，   
                     ”Transitions”：{   
                        ”NextAction”：{   
                           ”fbd09b5a-c04e--46c9--900f--3bcbfb693913”，   
                           ”Conditions”：{   
                              ”NextAction”：{   
                                 ”053786fc--1a9d--49bb--9f3b--0615313e7475”，   
                                 ”Condition”：{   
                                    ”Operator”：{  
                                       ”Equals”，  
                                       ”Operands”：[1]    
                                    }    
                                 }    
                              },    
                              {    
                                 ”NextAction”：{    
                                    ”3de54805-ed88--465a-b9d7--ced52cd08303”，    
                                    ”Condition”：{    
                                       ”Operator”：    
                                       {    
                                          ”Equals”，    
                                          ”Operands”：[2]    
                                       }    
                                    }    
                                 }    
                              },    
                              {    
                                 ”NextAction”：{    
                                    ”fbd09b5a-c04e--46c9--900f--3bcbfb693913”，    
                                    ”ErrorType”：{    
                                       ”InputTimeLimitExceeded”，    
                                       ”NoMatchingCondition”，    
                                       ”NoMatchingError”    
                                    }    
                                 }    
                              }    
                           ]     
                        }     
                     ]     
                  }     
                }     
              },     
              {     
                Parameters：{}，     
                Identifier：{}，     
                Type：{}，     
                Transitions：{}，     
              },     
              {     
                Parameters：{}，     
                Identifier：{}，     
                Type：{}，     
                Transitions：{}，     
              },     
              {     
                Parameters：{}，     
                Identifier：{}，     
                Type：{}，     
                Transitions：{}，     
              },     
              {     
                Parameters：{}，     
                Identifier：{}，     
                Type：{}，     
                Transitions：{}，     
              },      
              {      
                Parameters：{}，      
                Identifier：{}，      
                Type：{}，      
                Transitions：{}，      
              },      
              {      
                Parameters：{}，      
                Identifier：“24 d5690 d --cdf c --4 e17 -- a84 f --d018629 c 7 cf 8”，      
                Type：“MessageParticipant”，      
                Transitions：“NextAction”，“Errors”；      
              },      
              {      
                Parameters:{      
                  LambdaFunctionARN:“arn:aws:lambda:us-east:768637739934:function:Voice-to-chat-transfer”,      
                  InvocationTimeLimitSeconds:“8”,      
                  LambdaInvocationAttributes:{      
                    check:“mobile”      
                  },      
                  ResponseValidation:{      
                    ResponseType:“STRING_MAP”      
                  }      
                },      
                Identifier:“3de54805-ed88--465 a-b9d7--ced52cd08303”,      
                Type:“InvokeLambdaFunction”,      
                Transitions:{      
                  NextAction:“24 d5690 d --cdf c --4 e17 -- a84 f --d018629 c 7 cf 8”,      
                  Errors:{        
                    NextAction:“4750120 e --10 b0 --4 cd8 --92 af --664 d52233 b80”,        
                    ErrorType:“NoMatchingError”        
                  }        
                }        
              }]        
}

```