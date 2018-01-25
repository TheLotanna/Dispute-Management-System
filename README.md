# Dispute-Management-System
A system to receive customer requests and complaints

form Dispute_Management_System
{
	displayname = "Remita Dispute Management System"
	success message = "Data Added Successfully!"
	field alignment = left
	must have Your_Complain
	(
		type = radiobuttons
		displayname = "What would you like to complain about?"
		values = {"My payment failed", "I need a receipt", "I want a refund for a failed payment"}
		others option = true
		tooltip = "Please specify your complaint"
		width = 300px
		on user input
		{
			show Select_Channel;

		}
	)
	must have Select_Channel
	(
		type = picklist
		displayname = "On what channel did you do your transaction?"
		values = {"Card/Web", "Internet Banking", "Remita Mobile App", "POS", "Bank Branch", "Mobile Wallet (Paga, PocketMoni etc.)"}
		tooltip = "Select the payment channel used to process the transaction"
		width = 206px
		on user input
		{
			show Know_RRR;
			if(Know_RRR == "Yes")
			{
				show RRR;
			}
			else
			{
				hide RRR;
			}
			hide Payment_Details;
			hide Date_field;
			hide Amount;
			hide Payer_Name;
			hide Biller_Name;
			hide Funding_Account;
			hide Funding_Bank;
			hide Masked_PAN_6;
			hide Masked_PAN_4;
			hide Transaction_ID;
			if(Select_Channel == "Card/Web" || Select_Channel == "POS")
			{
				show Payment_Details;
				show Date_field;
				show Amount;
				show Masked_PAN_6;
				show Masked_PAN_4;
				show Biller_Name;
				show Payer_Name;
			}
			else if(Select_Channel == "Internet Banking" || Select_Channel == "Remita Mobile App")
			{
				show Payment_Details;
				show Date_field;
				show Amount;
				show Funding_Account;
				show Funding_Bank;
				show Biller_Name;
				show Payer_Name;
			}
			else if(Select_Channel == "Mobile Wallet (Paga, PocketMoni etc.)")
			{
				show Payment_Details;
				show Date_field;
				show Amount;
				show Transaction_ID;
				show Biller_Name;
				show Payer_Name;
			}
			else if(Select_Channel == "Bank Branch")
			{
				show Payment_Details;
				show Date_field;
				show Amount;
				show Funding_Bank;
				show Biller_Name;
				show Payer_Name;
			}

		}
	)
	Payment_Details
	(
    	type = plaintext
		value = "<hr /> <b>Please enter your payment details below</b>"
		width = 300px
	)
	must have Know_RRR
	(
		type = radiobuttons
		displayname = "Do you know your RRR?"
		values = {"Yes", "No"}
		layout = 2
		width = 300px
		on user input
		{
			show Complaint_For_Yourself;
			if(Know_RRR == "Yes")
			{
				show RRR;
			}
			else
			{
				hide RRR;
			}
			hide Payment_Details;
			hide Date_field;
			hide Amount;
			hide Payer_Name;
			hide Biller_Name;
			hide Funding_Account;
			hide Funding_Bank;
			hide Masked_PAN_6;
			hide Masked_PAN_4;
			hide Transaction_ID;
			if(Select_Channel == "Card/Web" || Select_Channel == "POS")
			{
				show Payment_Details;
				show Date_field;
				show Amount;
				show Masked_PAN_6;
				show Masked_PAN_4;
				show Biller_Name;
				show Payer_Name;
			}
			else if(Select_Channel == "Internet Banking" || Select_Channel == "Remita Mobile App")
			{
				show Payment_Details;
				show Date_field;
				show Amount;
				show Funding_Account;
				show Funding_Bank;
				show Biller_Name;
				show Payer_Name;
			}
			else if(Select_Channel == "Mobile Wallet (Paga, PocketMoni etc.)")
			{
				show Payment_Details;
				show Date_field;
				show Amount;
				show Transaction_ID;
				show Biller_Name;
				show Payer_Name;
			}
			else if(Select_Channel == "Bank Branch")
			{
				show Payment_Details;
				show Date_field;
				show Amount;
				show Funding_Bank;
				show Biller_Name;
				show Payer_Name;
			}

		}
	)
	RRR
	(
		type = number
		displayname = "Please enter your 12 digit RRR"
		maxchar = 12
		tooltip = "This is your Remita Retrieval Reference e.g. 123456789101"
		width = 200px
	)
	must have Date_field
	(
    	type = date
		displayname = "Date"
		alloweddays = 0,1,2,3,4,5,6
		tooltip = "Select the date your transaction was processed from the calendar"
		width = 200px
	)
	must have Amount
	(
		type = NGN
		maxchar = 13
		tooltip = "Input the transaction amount"
		width = 200px
	)
	must have Payer_Name
	(
    	type = text
		displayname = "Payer Name"
		tooltip = "Input the name of the payer"
		width = 200px
	)
	must have Biller_Name
	(
    	type = text
		displayname = "Biller Name (Beneficiary)"
		maxchar = 254
		tooltip = "This is the name of the organization you made payment to"
		width = 200px
	)
	Funding_Account
	(
		type = number
		displayname = "Funding Account Number"
		tooltip = "Input the account number the transaction was funded from"
		width = 200px
	)
	Funding_Bank
	(
		type = picklist
		displayname = "Funding Bank"
		values = {"Access Bank Plc", "Central Bank of Nigeria", "Citibank Nigeria Ltd", "Coronation Merchant Bank Ltd", "Diamond Bank Plc", "Ecobank Nigeria Plc", "Fidelity Bank Plc", "First City Monument Bank Plc", "FirstBank of Nigeria Plc", "FSDH Merchant Bank Ltd", "Guaranty Trust Bank Plc", "Heritage Bank Plc", "Jaiz Bank Plc", "Keystone Bank", "ProvidusBank Plc", "Skye Bank Plc", "Stanbic IBTC Bank Nigeria Ltd", "Standard Chartered Bank Nigeria Ltd", "Sterling Bank Plc", "Suntrust Bank Nigeria Ltd", "Union Bank of Nigeria Plc", "United Bank for Africa Plc", "Unity Bank Plc", "Wema Bank Plc", "Zenith Bank Plc"}
		tooltip = "Select the bank the transaction was funded from"
		width = 260px
	)
	Masked_PAN_6
	(
		type = number
		displayname = "First 6 digits of your card"
		maxchar = 6
		tooltip = "This is the first 6 digits of your card number e.g. 539983"
		width = 200px
	)
	Masked_PAN_4
	(
		type = number
		displayname = "Last 4 digits of your card"
		maxchar = 4
		tooltip = "This is the last 4 digits of your card number e.g. 4243"
		width = 200px
	)
	Transaction_ID
	(
    	type = text
		displayname = "Mobile Wallet Transaction ID"
		tooltip = "This is the mobile wallet (Paga, PocketMoni etc.) Transaction ID"
		width = 200px
	)
	must have Complaint_For_Yourself
	(
		type = radiobuttons
		displayname = "Are you making this complaint for yourself?"
		values = {"Yes", "No"}
		layout = 2
		width = 300px
		on user input
		{
			if(Complaint_For_Yourself == "Yes")
			{
				hide Contact_Details;
				hide Full_Name;
				hide Phone;
				show Email;
				show File_Upload;
				show Any_Comment;
			}
			else
			{
				show Contact_Details;
				show Full_Name;
				show Email;
				show Phone;
				show File_Upload;
				show Any_Comment;
			}

		}
	)
	Contact_Details
	(
    	type = plaintext
		value = "<b>Please enter the Payer&#39;s contact details below</b>"
		width = 300px
	)
	Full_Name
	(
    	type = text
		displayname = "Full Name"
		tooltip = "Input the Payer's full name"
		width = 200px
	)
	must have Email
	(
    	type = email
		displayname = "E-mail"
		tooltip = "Input the Payer's email address"
		width = 200px
	)
	Phone
	(
		type = number
		displayname = "Phone Number"
		maxchar = 11
		tooltip = "Input the Payer's phone number"
		width = 200px
	)
	Any_Comment
	(
    	type = richtext
		displayname = "Additional Details <i>(Optional)</i>"
		height = 200px
		toolbar = enable
		[
			style, strike-through, indent, font-color, background-color, remove-formatting, alignment, link, table, ruler, bullets-and-numbering, script-text, code, html, quote, 
			font-size : {1, 2, 3, 4, 5, 6, 7},
			font-family : {"Serif", "Arial", "Courier New", "Georgia", "Tahoma", "Times New Roman", "Trebuchet", "Verdana", "Comic Sans Ms"}
		]
		tooltip = "Kindly provide more information on your transaction (if any)"
		width = 506px
	)
	File_Upload
	(
    	type = upload file
		displayname = "Upload a file <i>(Optional)</i>"
				browse = local_drive, google_docs
		tooltip = "Upload screenshot, scanned document or other relevant files relating to your transaction"
		width = 300px
	)
	
			customize
			(
				label width = 330px
			)
	actions
	{
		on add
		{
			on load
			{
				hide Select_Channel;
				hide Know_RRR;
				hide RRR;
				hide Payment_Details;
				hide Date_field;
				hide Amount;
				hide Payer_Name;
				hide Biller_Name;
				hide Funding_Account;
				hide Funding_Bank;
				hide Masked_PAN_6;
				hide Masked_PAN_4;
				hide Transaction_ID;
				hide Complaint_For_Yourself;
				hide Contact_Details;
				hide Full_Name;
				hide Email;
				hide Phone;
				hide File_Upload;
				hide Any_Comment;

			}
			submit
			(
            	type = submit
            	displayname = "Submit"
		                         	PreSubmit  =  "<?xml version=\"1.0\" encoding=\"UTF-8\"?><preoncommit><openurl/><successmsg/></preoncommit>"
		                        	on success
		                        	{
		                                	success message "Thank you! We will review your request and get back to you shortly.";

		                        	}
			)
			reset
			(
            	type = reset
            	displayname = "Reset"
			)
		}
		on edit
		{
			update
			(
            	type = submit
            	displayname = "Update"
			)
			cancel
			(
            	type = cancel
            	displayname = "Cancel"
			)
		}
	}
	automation
	{
		tasks
		{
			New_Task as "New Task"
			{
				type : email
				from : Email
				to : "support@remita.net"
				subject : "Dispute Management System -  "+Your_Complain+""
				message : "<b><span class=\"zc-label-text\">What would you like to complain about?</span></b> "+Your_Complain+"<br /><br /><b><span class=\"zc-label-text\">On what channel did you do your transaction?<span class=\"fieldMandate\">&nbsp;</span></span></b> "+Select_Channel+"<br /><br /><b><span class=\"zc-label-text\">Do you know your RRR?</span></b> "+Know_RRR+"<br /><br /><b><label class=\"form-label zc-dem-clearfix zc-RRR-label  zc_number_label\"><span class=\"zc-label-text\">Please enter your 12 digit RRR</span></label> </b>"+RRR+"<br /><br /><span class=\"zc-label-text\"><b>Date</b><span class=\"fieldMandate\"></span></span> "+Date_field+"<br /><br /><b><span class=\"zc-label-text\">Amount<span class=\"fieldMandate\"></span></span></b> "+Amount+"<br /><br /><b><span class=\"zc-label-text\">Payer Name</span> </b>"+Payer_Name+"<br /><br /><span class=\"zc-label-text\"><b>Biller Name (Beneficiary)</b><span class=\"fieldMandate\"></span></span> "+Biller_Name+"<br /><br /><b>Funding Account Number </b>"+Funding_Account+"<br /><br /><b>Funding Bank</b> "+Funding_Bank+"<br /><br /><b>First 6 digits of your card </b>"+Masked_PAN_6+"<br /><br /><b>Last 4 digits of your card</b> "+Masked_PAN_4+"<br /><br /><b>Mobile Wallet Transaction ID</b> "+Transaction_ID+"<br /><br /><b>Are you making this complaint for yourself?</b> "+Complaint_For_Yourself+"<br /><br /><br /><b>Full Name</b> "+Full_Name+"<br /><br /><b>E-mail </b>"+Email+"<br /><br /><b>Phone</b> "+Phone+"<br /><br /><b>Comment</b> "+Any_Comment+"<br /><br /><b>Upload File</b> "+File_Upload+"<br />"
			}
		}
		rules
		{
				New_Rule as "Send Email on Success"
				{
					description : "Workflow"
					executeon	: add
					tasks		: [New_Task]
				}
		}
	}	
}
