2025-01-26T18:24:40.337Z
START RequestId: d080dac2-97a9-4bd4-9a1e-c1fe16582cc6 Version: $LATEST

START RequestId: d080dac2-97a9-4bd4-9a1e-c1fe16582cc6 Version: $LATEST
2025-01-26T18:24:40.367Z
2025-01-26T18:24:40.367Z	d080dac2-97a9-4bd4-9a1e-c1fe16582cc6	INFO	Received event: 
{
    "field": "messages",
    "value": {
        "sender": {
            "id": "12334"
        },
        "recipient": {
            "id": "23245"
        },
        "timestamp": "1527459824",
        "message": {
            "mid": "random_mid",
            "text": "random_text"
        }
    }
}


2025-01-26T18:24:40.367Z d080dac2-97a9-4bd4-9a1e-c1fe16582cc6 INFO Received event: {"field":"messages","value":{"sender":{"id":"12334"},"recipient":{"id":"23245"},"timestamp":"1527459824","message":{"mid":"random_mid","text":"random_text"}}}
2025-01-26T18:24:40.367Z
2025-01-26T18:24:40.367Z	d080dac2-97a9-4bd4-9a1e-c1fe16582cc6	INFO	Message from 12334: random_text

2025-01-26T18:24:40.367Z d080dac2-97a9-4bd4-9a1e-c1fe16582cc6 INFO Message from 12334: random_text
2025-01-26T18:24:40.367Z
2025-01-26T18:24:40.367Z	d080dac2-97a9-4bd4-9a1e-c1fe16582cc6	ERROR	Invoke Error 	
{
    "errorType": "ReferenceError",
    "errorMessage": "PAGE_ACCESS_TOKEN is not defined",
    "stack": [
        "ReferenceError: PAGE_ACCESS_TOKEN is not defined",
        "    at sendReplyToUser (file:///var/task/index.mjs:134:77)",
        "    at Runtime.handler (file:///var/task/index.mjs:114:22)",
        "    at Runtime.handleOnceNonStreaming (file:///var/runtime/index.mjs:1173:29)"
    ]
}


2025-01-26T18:24:40.367Z d080dac2-97a9-4bd4-9a1e-c1fe16582cc6 ERROR Invoke Error {"errorType":"ReferenceError","errorMessage":"PAGE_ACCESS_TOKEN is not defined","stack":["ReferenceError: PAGE_ACCESS_TOKEN is not defined"," at sendReplyToUser (file:///var/task/index.mjs:134:77)"," at Runtime.handler (file:///var/task/index.mjs:114:22)"," at Runtime.handleOnceNonStreaming (file:///var/runtime/index.mjs:1173:29)"]}
2025-01-26T18:24:40.427Z
END RequestId: d080dac2-97a9-4bd4-9a1e-c1fe16582
