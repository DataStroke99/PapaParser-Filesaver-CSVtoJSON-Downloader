# PapaParser + FileSaver - CSV to JSON Downloader


Welcome to this Papa Parse + FileSaverr Tutorial. I made this project as an experiment as i am trying to learn and work on bigger Javascript related applications. While working i needed to convert easily available CSV file sheets into JSON data, and stumbled onto the Paper Parser and FileSaver JS library.

PapaParser - is a great and powerful CSV Parser for JavaScript.

# HTML

Here is the body of the  HTML of the project:

	<form class="form-inline">
		<div class="form-group">
  			<label for="files">Upload a CSV formatted file:</label>
  				<input type="file" id="files"  class="form-control" accept=".csv" required />
		
 			<button type="submit" id="submit" class="btn btn-primary" >Submit</button>
 		</div>
	</form>
	

I form 2 buttons, one to upload the CSV file and other to download the converted JSON version of it.



# Javascript 

I use a jQuery  function attached to the download button.

First i conduct Error check, to make sure a CSV file has been uploaded if the user clicks on download  without uploading a file.

	<script type="application/javascript">
	
		$(document).ready(function(){
			
			$('#submit').on("click",function(e){
				e.preventDefault();
				if (!$('#files')[0].files.length){
					alert("Please choose at least one file to read the data.");
				}	
			
			var x = document.getElementById("files");
			Papa.parse(x.files[0],{
				header: true, complete: function(results)
        			{
					console.log("Parse results:", results.data);							
					var blob = new Blob([JSON.stringify(results.data)],{type: "application/json"});
					saveAs(blob,"download.json");
				}
			});	
		});	
	});

	</script>
				
Then i pass the file into the PapaParser function. to learn more about the library, the main website  -  https://www.papaparse.com/ has great documentation. But i found no example of what i was looking for , so after some experimentation i made this code.

In the PapaParser complete: function() the FileSaver.js  is used to download the converted JSON file. I integrated the Saving Text method from the FileSaver.js Documentation  -   https://github.com/eligrey/FileSaver.js/ . 

So once the user clicks the Download button, the JSON file would be downloaded on the User's device.


