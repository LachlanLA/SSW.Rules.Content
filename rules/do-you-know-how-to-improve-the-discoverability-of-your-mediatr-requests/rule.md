---
type: rule
archivedreason: 
title: Do you know how to improve the discoverability of your MediatR requests?
guid: 2aefa237-77d5-472d-bac7-c12f791aa802
uri: do-you-know-how-to-improve-the-discoverability-of-your-mediatr-requests
created: 2019-04-14T22:24:33.0000000Z
authors:
- id: 81
  title: Jason Taylor
related: []

---

When using MediatR within an ASP.NET Controller it is typical to see actions such as the following:

<!--endintro-->
<dl class="image">&lt;dt&gt;
      <img src="improve-mediatr-typical.png" alt="improve-mediatr-typical.png">
   &lt;/dt&gt;<dd>Figure: A Typical ASP.NET Controller using Mediator</dd></dl>
In the above example, the API contains a Create action that includes a CreateProductCommand parameter. This command is a request to create a new product, and the request is associated with an underlying request handler. The request is sent using MediatR with the method call \_mediator.Send(command). MediatR will match the request to the associated request handler and return the response (if any). In a typical implementation, the request and request handler would be contained within separate files:
<dl class="badImage">&lt;dt&gt;
      <img src="improve-mediatr-bad.png" alt="improve-mediatr-bad.png">
   &lt;/dt&gt;<dd>Figure: Bad Example - The request is contained within CreateProductCommand.cs<br></dd></dl><dl class="badImage">&lt;dt&gt;
      <img src="improve-mediatr-bad-2.png" alt="improve-mediatr-bad-2.png">
   &lt;/dt&gt;<dd>Figure: Bad Example - The request handler is contained within CreateProductCommandHandler.cs</dd></dl>
In the above implementation, the request handler is cleanly separated from the request. However, this separation results in reducing discoverability of the handler. For example, a developer looking at the action in this first figure might be interested in the logic behind the command. So, they press F12 to go to the definition and can see the request (CreateProductCommand), but not the logic since it is contained within the request handler (CreateProductCommandHandler). The developer must then navigate to the handler using Solution Explorer or some keyboard wizardry. This is assuming that the developer is familiar with the design, and knows that there is an underlying request handler that contains the logic of interest. We can avoid these problems and improve discoverability by instead using the following approach:
<dl class="goodImage">&lt;dt&gt;
      <img src="improve-mediatr-good.png" alt="business-logic-presentation-layer-good.png">
   &lt;/dt&gt;<dd>Figure: Good Example - Nesting the Request Handler within the Request Improves Discoverability of Command and Associated Command Logic</dd></dl>
In the above example the request handler is nested within the request, there by improving the discoverability of the command and associated command logic.