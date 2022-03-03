# ServerSideEvent
```
<a href="javascript:initialize();" >Click Me To See Magic</a>  
<div id="targetDiv"></div>  
  
<script>  
      
    function initialize() {  
        alert("called");  
  
        if (window.EventSource == undefined) {  
            // If not supported  
            document.getElementById('targetDiv').innerHTML = "Your browser doesn't support Server Sent Events.";  
            return;  
        } else {  
            var source = new EventSource('../Home/Message');  
  
            source.onopen = function (event) {  
                document.getElementById('targetDiv').innerHTML += 'Connection Opened.<br>';  
            };  
  
            source.onerror = function (event) {  
                if (event.eventPhase == EventSource.CLOSED) {  
                    document.getElementById('targetDiv').innerHTML += 'Connection Closed.<br>';  
                }  
            };  
  
            source.onmessage = function (event) {  
                document.getElementById('targetDiv').innerHTML += event.data + '<br>';  
            };  
        }  
    }  
</script> 
```

```
public void Message()  
{  
    Response.ContentType = "text/event-stream";  
  
    DateTime startDate = DateTime.Now;  
    while (startDate.AddMinutes(1) > DateTime.Now)  
    {  
        Response.Write(string.Format("data: {0}\n\n", DateTime.Now.ToString()));  
        Response.Flush();  
  
        System.Threading.Thread.Sleep(1000);  
    }  
      
    Response.Close();  
} 
```

References 
https://www.c-sharpcorner.com/blogs/server-side-events-in-asp-net-mvc

https://makolyte.com/aspnet-async-sse-endpoint/
