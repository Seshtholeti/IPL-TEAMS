
import fetch from 'node-fetch';
export const handler = async (event) => {
   const VERIFY_TOKEN = "token_123";
   const PAGE_ACCESS_TOKEN = "EAAX8zKLRFn8BO4NcgAnFzaHkFQq116F0JY1cMzJSMyeo8IRmglZBbP4TxwEmGqvprQmZCkg8JKSaylI2o066YYUaFxOntbeHChZCO4D3hAPBHQgMZA5YZCzzwUItHWCaG6u0sRF9HmKVsAC31gsFSHNIZB93ZAJBx4DhTjTNW3HygQwma0eeYEa914HLnRHCwEVKgZDZD";
   // Handle GET Request (Webhook Validation)
   if (event.httpMethod === "GET") {
       const params = event.queryStringParameters;
       if (params["hub.mode"] === "subscribe" && params["hub.verify_token"] === VERIFY_TOKEN) {
           return {
               statusCode: 200,
               body: params["hub.challenge"], // Return the challenge value
           };
       }
       return { statusCode: 403, body: "Forbidden - Validation Failed" }; // Invalid token or mode
   }
   // Handle POST Request (Incoming Events)
   if (event.httpMethod === "POST") {
       const body = JSON.parse(event.body);
       // Log the received event payload to understand its structure
       console.log("Received event:", JSON.stringify(body));
       // Check if object field is present and it's 'instagram'
       if (body.object === "instagram") {
           // Loop through the 'entry' array
           body.entry.forEach((entry) => {
               if (entry.changes) {
                   entry.changes.forEach((change) => {
                       // Log the change to examine its structure
                       console.log("Received change:", JSON.stringify(change));
                       // Handling message events from Instagram
                       if (change.field === "messages") {
                           const senderId = change.value.sender.id;
                           const text = change.value.message.text;
                           console.log(`Message from ${senderId}: ${text}`);
                           // Send a reply to the user (example)
                           sendReplyToUser(senderId, `You said: "${text}"`);
                       } else {
                           console.warn(`Unsupported field: ${change.field}`);
                       }
                   });
               }
           });
           return {
               statusCode: 200,
               body: "EVENT_RECEIVED",
           };
       } else {
           console.warn(`Unsupported object: ${body.object}`);
           return {
               statusCode: 404,
               body: "Unsupported Event Type",
           };
       }
   }
   return { statusCode: 404, body: "Unsupported HTTP Method" };
};
// Function to Send a Reply to the User
async function sendReplyToUser(senderId, message) {
   const url = `https://graph.facebook.com/v16.0/me/messages?access_token=${PAGE_ACCESS_TOKEN}`;
   const body = {
       recipient: { id: senderId },
       message: { text: message },
   };
   try {
       const response = await fetch(url, {
           method: "POST",
           headers: { "Content-Type": "application/json" },
           body: JSON.stringify(body),
       });
       const data = await response.json();
       console.log("Reply sent successfully:", data);
   } catch (error) {
       console.error("Error sending reply:", error);
   }
}



this is the logs for above lambda.

2025-01-26T18:17:10.267Z
START RequestId: 342cf0a0-9e9c-4ab1-8f50-2a4cfcecd6b5 Version: $LATEST

START RequestId: 342cf0a0-9e9c-4ab1-8f50-2a4cfcecd6b5 Version: $LATEST
2025-01-26T18:17:10.268Z
2025-01-26T18:17:10.268Z	342cf0a0-9e9c-4ab1-8f50-2a4cfcecd6b5	INFO	Received event: 
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


2025-01-26T18:17:10.268Z 342cf0a0-9e9c-4ab1-8f50-2a4cfcecd6b5 INFO Received event: {"field":"messages","value":{"sender":{"id":"12334"},"recipient":{"id":"23245"},"timestamp":"1527459824","message":{"mid":"random_mid","text":"random_text"}}}
2025-01-26T18:17:10.268Z
2025-01-26T18:17:10.268Z	342cf0a0-9e9c-4ab1-8f50-2a4cfcecd6b5	WARN	Unsupported object: undefined




you know thw sample payload how it will be from meta
