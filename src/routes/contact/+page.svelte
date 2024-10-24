       
    <svelte:head>
        <title>This is my contact page!</title>
    </svelte:head>
    
    <h1>This is my contact page!</h1>
    <form action="mailto:filinanurcahya0000@gmail.com" method="POST" enctype="text/plain">
        <label for="email">Your Email:</label>
        <input id="email" name="email" type="email" required>
        
        <label for="subject">Subject:</label>
        <input id="subject" name="subject" required>
        
        <label for="body">Message:</label>
        <textarea id="body" name="body" rows="5" cols="30" required></textarea>
        
        <button type="submit">Submit</button>
    </form>
 