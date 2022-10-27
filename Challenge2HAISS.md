# WidgetApp Article (Draft)

Anonymous Ltd. has developed a new Streaming API (also known as HTTP Push) that lets you
design **Things**. 

## Overview 

Users scroll through the homepage of WidgetApp, and then selects a **Thing**.
Once selected, they can start working on it using the editor. Most actions of the editor
work by calling AJAX (Asynchronous JavaScript and XML) endpoints, allowing updates without
having to reload the web page. 

## Streaming frontend (SFE)

Because this API is streaming over WebSocket, exposing real-time data, multiple users
can simultaneously work on the same **Thing**. It's important that any changes made are 
quickly communicated so that they can be seen by all clients. 

## Connection details

In order to communicate using WebSocket, you'll need to create a `WebSocket` object which
will attempt to open the connection to the server. 
Authentication is done over a secure WSS protocol and the URL to which to connect is
wss://www.widgetapp.com/_stream.

The initial request made by the API goes to [Cloudflare] (https://www.cloudflare.com/),
then routed to the SFE. 

### Multiple services on one WebSocket connection

Different services can use the same WebSocket connection. How this works is, the
Streaming frontend:

1. Accepts the connection at the server.
2. Using its filter chain, builds the request context.
3. Splits the stream by the service.
4. Connects them to the corresponding services. 

# How I approached creating this article from my notes

Firstly, for this article, I thought about the order of content that the reader would be 
able to learn more about the new Streaming API. I believe an overview, describing what it 
is and why or how it's used is important to start out with. I did some research on how 
Streaming APIs and WebSocket works in order to effectively communicate details about 
connection. I'm assuming that a building WebSocket API from scratch was not necessary and
describing how this is done is already known by the audience being familiar with 
WidgetApps other APIs. 

## Questions and missing details to complete the Article

1. It would be helpful to show an example of or available AJAX endpoints. Since users are
   first interacting with the editor, perhaps available editor actions would be useful.
2. Should there be more details on authentication?
3. What format can responses be in? Should examples be provided? 