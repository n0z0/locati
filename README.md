# Location Based Testing
You're correct; the `Cookie` header is missing in the example. Here's an updated version that includes the `Cookie` header as well.

```go
package main

import (
	"bytes"
	"fmt"
	"io"
	"mime/multipart"
	"net/http"
)

func main() {
	// URL to send the POST request
	url := "https://siakad.ulbi.ac.id/hr/home"

	// Prepare the form data
	var buffer bytes.Buffer
	writer := multipart.NewWriter(&buffer)

	// Setting up the boundaries as in the provided example
	boundary := "----WebKitFormBoundarydoh0aqA1vN4uIUtQ"
	writer.SetBoundary(boundary)

	// Add form fields
	fields := map[string]string{
		"foto":            "",
		"keterangan":      "",
		"_wysihtml5_mode": "1",
		"act":             "clock",
		"latitude":        "-6.8739858",
		"longitude":       "107.5756769",
		"lokasi":          "Anda berada di [Kampus ULBI]",
		"issetlocation":   "1",
		"isgedung":        "1",
		"isluarlokasi":    "0",
	}

	for key, val := range fields {
		_ = writer.WriteField(key, val)
	}

	// Close the writer to finalize the form data
	writer.Close()

	// Creating a new HTTP request
	req, err := http.NewRequest("POST", url, &buffer)
	if err != nil {
		fmt.Println("Error creating request:", err)
		return
	}

	// Set headers as per your provided screenshot
	req.Header.Set("Content-Type", "multipart/form-data; boundary="+boundary)
	req.Header.Set("Accept", "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7")
	req.Header.Set("Accept-Encoding", "gzip, deflate, br, zstd")
	req.Header.Set("Accept-Language", "en-US,en;q=0.9,id;q=0.8")
	req.Header.Set("Cache-Control", "no-cache")
	req.Header.Set("Origin", "https://siakad.ulbi.ac.id")
	req.Header.Set("Pragma", "no-cache")
	req.Header.Set("Referer", "https://siakad.ulbi.ac.id/hr/home")
	req.Header.Set("Sec-Ch-Ua", `"Chromium";v="130", "Google Chrome";v="130", "Not?A Brand";v="99"`)
	req.Header.Set("Sec-Ch-Ua-Mobile", "?0")
	req.Header.Set("Sec-Ch-Ua-Platform", `"Windows"`)
	req.Header.Set("Sec-Fetch-Dest", "document")
	req.Header.Set("Sec-Fetch-Mode", "navigate")
	req.Header.Set("Sec-Fetch-Site", "same-origin")
	req.Header.Set("Sec-Fetch-User", "?1")
	req.Header.Set("Upgrade-Insecure-Requests", "1")
	req.Header.Set("User-Agent", "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36")

	// Set the Cookie header as per the screenshot
	req.Header.Set("Cookie", "_ga_B7YLH1E9RC=GS1.1.1702407242.4.0.1702407242.0.0.0; _tt_enable_cookie=1; _ttp=clm8e9iPZinouyHQOomveSnISVN; _ga_TH39B9SDQC=GS1.1.1716998012.1.0.1716998072.0.0.0; _fbp=fb.2.1724474588063.714205733685158143; _ga_ER9K9TX7NF=GS1.1.1724484619.6.0.1724484619.0.0.0; _gid=GA1.3.1659531982.1730934317; _clsk=1uujof6or%7C1730935571943%7Ct0%7Cf.clarity.ms%2Fcollect; _ga_9G5ZKCDXCH=GS1.1.1730934318.15.1.1730934870.0.5.0; _ga_1F0NKMSQDL=GS1.1.1730934317.15.1.1730935597.0.0")

	// Make the HTTP request
	client := &http.Client{}
	resp, err := client.Do(req)
	if err != nil {
		fmt.Println("Error making request:", err)
		return
	}
	defer resp.Body.Close()

	// Read the response
	body, err := io.ReadAll(resp.Body)
	if err != nil {
		fmt.Println("Error reading response:", err)
		return
	}

	// Print response body
	fmt.Println(string(body))
}
```

### Explanation of Changes
1. **Cookie Header**: Added the `Cookie` header with the exact value from the screenshot. This header contains various cookies like `_ga_B7YLH1E9RC`, `_tt_enable_cookie`, `_ttp`, and others, each separated by a semicolon.

2. **HTTP Client**: The rest of the code remains the same, sending the request with all headers, including `Cookie`, to make the request as close to the one shown in the screenshot as possible.

This should match your requirements exactly, sending all the headers and cookies specified. Let me know if there’s anything else!
