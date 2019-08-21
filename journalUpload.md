**JournalUpload**
----
	Returns "success" and a count of uploaded journals, or a structure of invalid validations "__invalid" belonging to these journals.
	
* **Version History:**

	TASS v51.4 - Method Added

* **Version:**

	2

* **Method:**

	`GET | POST`
	
*  **Params:**

	**Required:**

	`year [number]` - year.

	`period [number]` - period.

	`line_items [array]` - an array of journal line items.

		7 items are required in each journal line items:

		`seq_num [number]` - the line/sequence number.

		`acct_code [string]` - a valid GL account code.

		`trans_desc [string]` - a detailed transaction description.

		`analy_text [string]` - an analysis description.

		`debit_amt [number]` - the amount to be debited.

		`credit_amt [number]` - the amount to be credited.

		`source [string]` - the source of the journal line items.

	**Optional:**
	
	`comment_1 [string]` - comment 1.

	`comment_2 [string]` - comment 2.

	**Conditional:**
	
	`control_amt [number]` - control amount.

* **Success Response:**

	```javascript
	{
		"success": "You successfully uploaded 2 line items.",
		"token": {
			"year": 2019,
			"period": 8,
			"timestamp": "{ts '2019-08-21 14:01:26'}",
			"comment_2": "Comment 2",
			"comment_1": "Comment 1",
			"line_items": [
				{
					"debit_amt": 100,
					"seq_num": 1,
					"acct_code": "01-0115-00-00",
					"credit_amt": 0,
					"source": "UPLOAD",
					"trans_desc": "Desc1-Transaction Description",
					"analy_text": "Desc2-Analysis"
				},
				{
					"debit_amt": 0,
					"seq_num": 2,
					"acct_code": "01-0112-00-00",
					"credit_amt": 100,
					"source": "UPLOAD",
					"trans_desc": "Desc1-Transaction Description",
					"analy_text": "Desc2-Analysis"
				}
			]
		}
	}
	```
 
* **Error Response:**

	`year` not supplied
	```javascript
	__invalid: {
		"year": "field is required"
	}
	```

	`period` not supplied
	```javascript
	__invalid: {
		"period": "field is required"
	}
	```

	`line_items` not supplied
	```javascript
	__invalid: {
		"line_items": "field is required"
	}
	```

	`control_amt` not supplied if control_tot_flag = "Y"
	```javascript
	__invalid: {
		"control_amt": "field is required"
	}
	```

	`control_amt` not a number if supplied
	```javascript
	__invalid: {
		"control_amt": "invalid amount"
	}
	```

	`control_amt` equal to 0 if supplied
	```javascript
	__invalid: {
		"control_amt": "control_amt must be larger than 0 if control_tot_flag has set to 'Y'."
	}
	```

	`year` not between 1900 and 2100
	```javascript
	__invalid: {
		"year": "The year must be between 1900 and 2100."
	}
	```

	`year` not a number
	```javascript
	__invalid: {
		"year": "Value is not a valid number."
	}
	```

	`period` not a number
	```javascript
	__invalid: {
		"period": "Value is not a valid number."
	}
	```

	`year/period` not set up
	```javascript
	__invalid: {
		"Year/Period": "Accounting Period is closed or not set up."
	}
	```

	`comment_1` not set up
	```javascript
	__invalid: {
		"comment_1": "Comment 1 cannot have more than 40 characters."
	}
	```

	`comment_2` not set up
	```javascript
	__invalid: {
		"comment_2": "Comment 2 cannot have more than 40 characters."
	}
	```

	`line_items` has only one line item
	```javascript
	__invalid: {
		"line_items": "Must have at least 2 line_items."
	}
	```

	`line_items` has only one line item
	```javascript
	__invalid: {
		"line_items": "Must have at least 2 line_items."
	}
	```

	`seq_num` has only one line item
	```javascript
	__invalid: {
		"line_items 1": "seq_num must be included in line_items."
	}
	```

	`acct_code` has only one line item
	```javascript
	__invalid: {
		"line_items 1": "acct_code must be included in line_items."
	}
	```

	`trans_desc` has only one line item
	```javascript
	__invalid: {
		"line_items 1": "trans_desc must be included in line_items."
	}
	```

	`analy_text` has only one line item
	```javascript
	__invalid: {
		"line_items 1": "analy_text must be included in line_items."
	}
	```

	`debit_amt` has only one line item
	```javascript
	__invalid: {
		"line_items 1": "debit_amt must be included in line_items."
	}
	```

	`credit_amt` has only one line item
	```javascript
	__invalid: {
		"line_items 1": "credit_amt must be included in line_items."
	}
	```

	`source` has only one line item
	```javascript
	__invalid: {
		"line_items 1": "source must be included in line_items."
	}
	```

	`seq_num` is not an integer
	```javascript
	__invalid: {
		"line_items 1": "Sequence number must be an integer."
	}
	```

	`seq_num` is not in correct sequence format, must be unique numbers 1,2,3,... not necessarily in order
	```javascript
	__invalid: {
		"line_items": "Sequence numbers are incorrect"
	}
	```

	`debit_amt` and `credit_amt` cannot be equal to or greater than 0 at the same time for one line item
	```javascript
	__invalid: {
		"line_items": "Debit and Credit amounts cannot both be greater than zero on the same line"
	}
	```

	`debit_amt` and `credit_amt` sums are not equal
	```javascript
	__invalid: {
		"line_items": "Sum of Debit amounts ([Debit Sum]) does not equal sum of Credit amounts ([Credit Sum])"
	}
	```

* **Sample Parameters:**

	```javascript
		{
			"year":"2019",
			"period":"8",
			"comment_1":"Comment 1",
			"comment_2":"Comment 2",
			"line_items":[
				{
					"seq_num":"1",
					"acct_code":"01-0115-00-00",
					"trans_desc":"Desc1-Transaction Description",
					"analy_text":"Desc2-Analysis",
					"debit_amt":"100.00",
					"credit_amt":"0.00",
					"source":"UPLOAD"
				},
				{
					"seq_num":"2",
					"acct_code":"01-0112-00-00",
					"trans_desc":"Desc1-Transaction Description",
					"analy_text":"Desc2-Analysis",
					"debit_amt":"0.00",
					"credit_amt":"100.00",
					"source":"UPLOAD"
				}
			]
		}
	```

* **Sample GET:** (With URL Encoded `token`)

	```HTML
	http://api.tasscloud.com.au/tassweb/api/?method=journalUpload&appcode=API21&company=10&v=2&token=BJVvYXC0We4Dtvp6Q49RqhBeAi6uqpTQ9t%2FKI9ZAFpCMeVXIFlDU5yNQIeYME%2BYLXgYA69RTUjXjLeVBetN6CaFMdPCKMWBXD%2Bkkt0%2Fuht0suYrSDONP6mx%2Fbt4WGgNOD5YoIYRNiIVDw2Qn2Oi5YodaEUgtGJohUJMzy3tqsX%2BraZk3j7d77okDCjb7MeFJ0DcupqUoRiGjE39415HTfPgNc6R6BY9wt7SJsj4yOPBrIxHQVS8Yy6gZ3nZgsJ5rhcdkB6eCI6b3FJ31s6vsVcbVu5NBY8AF1qqjWLMazduISzEBwRDsofXfJjo1KLX59R410bmbrF5Z7QZfEfE%2FlettTWOyb4EgdhBoC3v0aLOfF6Bt12AFXDo2VGbgryceeOLAscp%2FFr9ttH42hClBtWsxFU1N5dDENUsVHOwWcfCxd7aTtc0xjvaEYJWcZrRRZa1yrIvgeWaDk0LVxM5ePcT%2BltdrymgmxmZYgxdiYC1qQDcNXDx9hN7yKeZDUztwGA0yl2iXW8aBXAy5hRnztR0TrREyOba26mUHxUJO7tfpIyOrpPbE0nR18vtCZ%2BinbvyqN9adpZhQPByG2XD9M6MoYdmBCc3Duv9qb%2BIa0A8%3D
	```
	
* **Sample POST:**

	```HTML
	<form id="postForm" name="postForm" method="POST" action="http://api.tasscloud.com.au/tassweb/api/">
		 <input type="hidden" name="method" value="journalUpload">
		 <input type="hidden" name="appcode" value="API21">
		 <input type="hidden" name="company" value="10">
		 <input type="hidden" name="v" value="2">
		 <textarea name="token">BJVvYXC0We4Dtvp6Q49RqhBeAi6uqpTQ9t/KI9ZAFpCMeVXIFlDU5yNQIeYME+YLXgYA69RTUjXjLeVBetN6CaFMdPCKMWBXD+kkt0/uht0suYrSDONP6mx/bt4WGgNOD5YoIYRNiIVDw2Qn2Oi5YodaEUgtGJohUJMzy3tqsX+raZk3j7d77okDCjb7MeFJ0DcupqUoRiGjE39415HTfPgNc6R6BY9wt7SJsj4yOPBrIxHQVS8Yy6gZ3nZgsJ5rhcdkB6eCI6b3FJ31s6vsVcbVu5NBY8AF1qqjWLMazduISzEBwRDsofXfJjo1KLX59R410bmbrF5Z7QZfEfE/lettTWOyb4EgdhBoC3v0aLOfF6Bt12AFXDo2VGbgryceeOLAscp/Fr9ttH42hClBtWsxFU1N5dDENUsVHOwWcfCxd7aTtc0xjvaEYJWcZrRRZa1yrIvgeWaDk0LVxM5ePcT+ltdrymgmxmZYgxdiYC1qQDcNXDx9hN7yKeZDUztwGA0yl2iXW8aBXAy5hRnztR0TrREyOba26mUHxUJO7tfpIyOrpPbE0nR18vtCZ+inbvyqN9adpZhQPByG2XD9M6MoYdmBCc3Duv9qb+Ia0A8=</textarea>
	</form>
	```
