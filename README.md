
# cod-seriel

# cod-seriel
<!doctype html= are>
	<head>
		<style>
			/* CSS comes here */
			body {
			    font-family: arial;
			}
			button {
			    padding:10px;
			    background-color:#c7ce67;
			    color: #da2d2d;
			    border: 0px;
			    cursor:pointer;
			    border-radius: 5px;
			}
			#output {
			    background-color:#f9f9f9;
			    padding:10px;
			    width: 100%;
			    margin-top:20px;
			    line-height:30px;
			}
			.hide {
			    display:none;
			}
			.show {
			    display:block;
		/* CSS comes here */
		
		body {
			font-family: arial;
		}

		<p><span id="action"></span></p>
		<div id="output" class="hide"></div>
			}
		</style>
		<title>تحويل الصوت  لكتابه</title>
	</head>
	<body>
	<meta charset="UTF-8">
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
	
					

		<h2>تحويل الصوت </h2>
        <p>اضغط علي الزر وتحدث...</p>
        <p><button type="button" onclick="runSpeechRecognition()">Speech to Text</button> &nbsp; <span id="action"></span></p>
        <div id="output" class="hide"></div>
        

		
		<button class="button-71" role="button" id="button" >connect</button><br>
	
		<script>
			/* JS comes here */
	
			document.querySelector('#button').addEventListener('click', async () => {
	
				port = await navigator.serial.requestPort();
				await port.open({ baudRate: 9600 });
	
	
			});
			
				function stt(){
					// get output div reference
					var output = document.getElementById("output");
					// get action element reference
					var action = document.getElementById("action");
					// new speech recognition object
					var SpeechRecognition = SpeechRecognition || webkitSpeechRecognition;
					var recognition = new SpeechRecognition();            
					// This runs when the speech recognition service starts
					recognition.onstart = function() {
						action.innerHTML = "<small>listening, please speak...</small>";
					};
					
					recognition.onspeechend = function() {
						action.innerHTML = "<small>stopped listening</small>";
						recognition.stop();
					}
				  
					// This runs when the speech recognition service returns result
					recognition.onresult = function(event) {
						var transcript = event.results[0][0].transcript;
						output.innerHTML = transcript ;
						output.classList.remove("hide");
						
						if(transcript == "يمين"){
							console.log(transcript);
							send("right");
						}else if(transcript == "يسار"){
							console.log(transcript);
							send("left");					
						}
						
						
					};		
					 // start recognition
					 recognition.start();
		
				}		
	
				async function send(text){
					const textEncoder = new TextEncoderStream();
					const writableStreamClosed = textEncoder.readable.pipeTo(port.writable);
					const writer = textEncoder.writable.getWriter();
					await writer.write(text);
					writer.close();
					await writableStreamClosed;			
				}
				
	

	
	
		
		

		
		
		/* JS comes here */

		document.querySelector('#button').addEventListener('click', async () => {

			port = await navigator.serial.requestPort();
			await port.open({ baudRate: 9600 });


		});
		
			function stt(){
		        // get output div reference
		        var output = document.getElementById("output");
		        // get action element reference
		        var action = document.getElementById("action");
                // new speech recognition object
                var SpeechRecognition = SpeechRecognition || webkitSpeechRecognition;
                var recognition = new SpeechRecognition();            
                // This runs when the speech recognition service starts
                recognition.onstart = function() {
                    action.innerHTML = "<small>listening, please speak...</small>";
                };
                
                recognition.onspeechend = function() {
                    action.innerHTML = "<small>stopped listening</small>";
                    recognition.stop();
                }
              
                // This runs when the speech recognition service returns result
                recognition.onresult = function(event) {
                    var transcript = event.results[0][0].transcript;
                    output.innerHTML = transcript ;
                    output.classList.remove("hide");
					
					if(transcript == "يمين"){
						console.log(transcript);
						send("right");
					}else if(transcript == "يسار"){
						console.log(transcript);
						send("left");					
					}
					
					
                };		
                 // start recognition
                 recognition.start();
	
			}		

			async function send(text){
				const textEncoder = new TextEncoderStream();
				const writableStreamClosed = textEncoder.readable.pipeTo(port.writable);
				const writer = textEncoder.writable.getWriter();
				await writer.write(text);
				writer.close();
				await writableStreamClosed;			
			}



		</script>
		
	
	
	
	
		<script>
			/* JS comes here */
		    function runSpeechRecognition() {
		        // get output div reference
		        var output = document.getElementById("output");
		        // get action element reference
		        var action = document.getElementById("action");
                // new speech recognition object
                var SpeechRecognition = SpeechRecognition || webkitSpeechRecognition;
                var recognition = new SpeechRecognition();
            
                // This runs when the speech recognition service starts
                recognition.onstart = function() {
                    action.innerHTML = "<small>listening, please speak...</small>";
                };
                
                recognition.onspeechend = function() {
                    action.innerHTML = "<small>stopped listening, hope you are done...</small>";
                    recognition.stop();
                }
              
                // This runs when the speech recognition service returns result
                recognition.onresult = function(event) {
                    var transcript = event.results[0][0].transcript;
                    var confidence = event.results[0][0].confidence;
                    output.innerHTML = "<b>Text:</b> " + transcript + "<br/> <b>Confidence:</b> " + confidence*100+"%";
                    output.classList.remove("hide");
                };
              
                 // start recognition

                 recognition.start();
	        }
		</script>
<script>
	/*js comes here */
	
		
		
		document.querySelector('button').addEventListener('click', async () => {
// Prompt user to select any serial port.
const port = await navigator.serial.requestPort();
while (port.readable) {
const reader = port.readable.getReader();

try {
while (true) {
const { value, done } = await reader.read();
if (done) {
// Allow the serial port to be closed later.
reader.releaseLock();
break;
}
if (value) {
console.log(value);
}
}
} catch (error) {
// TODO: Handle non-fatal read error.
}
}const writer = port.writable.getWriter();

const data = new Uint8Array([104, 101, 108, 108, 111]); // hello
await writer.write(data);


// Allow the serial port to be closed later.
writer.releaseLock();
	  
		 

	

	

	
</script>






	</body>
</html>
