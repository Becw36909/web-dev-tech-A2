# s3903758-s3644527-a2

Web Development Technologies, Assignment 2

Group 7 Contributors: Rebecca Watson - s3903758, Christopher Orrell - s3644527

GitHub Repository URL: https://github.com/rmit-wdt-sp2-2023/s3903758-s3644527-a2

Project Description:
This project is an ASP.NET Core MVC Website for Internet
Banking with .NET 7.0 written in C# using Visual Studio 2022 with an Azure Microsoft
SQL Server database, for the client MCBA (Most Common Bank of Australia). All 
database operations have been completed using Entity Framework Core.
The compeleted solution includes a Customer website, an Admin website, and a WebAPI. 

Project Goal:
After the MCBA (Most Common Bank of Australia) was impressed with the initial console
application delivered by the Group 7 contributors Rebecca and Christopher, the client
requested an Internet Banking website to be designed complete with front end UI and 
backend operations communicating with a database for the following features:
• Check account balance and transaction history.
• Simulate transactions such as deposits and withdrawals.
• Transfer money between accounts.
• Schedule payments.
• Modify a personal profile.
• Perform administrative tasks.  


ASP.NET Core Web API Documentation:
Project Name: MCBAWebAPI
Implemented using the Repository design pattern.

## Endpoints - CustomerController
1.
https://localhost:7290/api/customer
Method:
    // GET: api/customer
    [HttpGet]
    public IEnumerable<Customer>Index()
    {
        return _repo.GetAllCustomers();
    }

### Retrieves All Customers

Retrieves a list of all customers.

- **Method:** GET
- **URL:** `/api/customer`

**Response:**

- **Status 200 OK**
  - Returns a list of all customers.

2.
https://localhost:7290/api/customer/2100 (example customerID)
Method:
    // GET api/customer/1
    [HttpGet("{customerID}")]
    public Customer Show(int CustomerID)
    {
        return _repo.GetCustomer(CustomerID);
    }

### Retrieves Customer Information

Retrieves a single customer's information by ID.

- **Method:** GET
- **URL:** `/api/customer/{customerID}`

**Parameters:**

- `customerID` (integer) - The ID of the customer to retrieve.

**Response:**

- **Status 200 OK**
  - Returns the customer information if found.

- **Status 404 Not Found**
  - If no customer is found with the given ID.

3. 
https://localhost:7290/api/customer/2100 (example customerID)
Method:
      // Post api/customer/1
    [HttpPost("{customerID}")]
    public void Update([FromBody] Customer customer)
    {
        // check that customer exists, return error if doesn't
        _repo.UpdateCustomer(customer.CustomerID, customer);
    }

### Update Customer Information

Updates customer information.

- **Method:** POST
- **URL:** `/api/customer/{customerID}`

**Parameters:**

- `customerID` (integer) - The ID of the customer to update.

**Request Body:**

The request body should contain a JSON object with updated customer information fields.

**Response:**

- **Status 204 No Content**
  - If the customer information is updated successfully.

4. 
https://localhost:7290/api/customer/toggleAccess/2100 (example customerID)
Method:
  // Get api/customer/toggleAccess/{customerID}
    [HttpGet("toggleAccess/{customerID}")]
    public void ToggleAccess(int customerID)
    {
        if (customerID != null)
        {
            Customer Customer = _repo.GetCustomer(customerID);

            Customer.ToggleAccess();
            _repo.CustomerAccess(customerID, Customer);
        }
    }

### Toggle Customer Access

Toggles customer access status.

- **Method:** GET
- **URL:** `/api/customer/toggleAccess/{customerID}`

**Parameters:**

- `customerID` (integer) - The ID of the customer to toggle access for.

**Response:**

- **Status 204 No Content**
  - If customer access status is toggled successfully.


## Endpoints - BillPayController
1.
https://localhost:7290/api/billpay
Method:
    // GET: api/billpay
    [HttpGet]
    public IEnumerable<BillPay> Index()
    {
        return _repo.GetAllBillPays();
    }

### Retrieve All BillPays

Retrieves a list of all BillPay payments.

- **Method:** GET
- **URL:** `/api/billpay`

**Response:**

- **Status 200 OK**
  - Returns a list of all BillPay payments.

2.
https://localhost:7290/api/billpay/toggleBlock/30 (example BillPayID)
Method:
   // Get api/billpay/toggleBlock/{billpayID}
    [HttpGet("toggleBlock/{billpayID}")]
    public void ToggleAccess(int billpayID)
    {
        if (billpayID != null)
        {
            BillPay Billpay = _repo.GetBillPay(billpayID);

            Billpay.ToggleBlock();

            _repo.UpdateBillPay(billpayID, Billpay);
        }

    }

### Toggle BillPay Block

Toggles the block status of a BillPay payment.

- **Method:** GET
- **URL:** `/api/billpay/toggleBlock/{billpayID}`

**Parameters:**

- `billpayID` (integer) - The ID of the BillPay payment to toggle block status for.

**Response:**

- **Status 204 No Content**
  - If BillPay payment block status is toggled successfully.

  