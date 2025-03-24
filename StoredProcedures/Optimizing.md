# Optimizing Stored Procedures for GitHub Copilot

## Prompt 1: Basic SQL Stored Procedure Optimization
```
Intent: To help developers optimize simple SQL stored procedures using GitHub Copilot.

Context: You have a SQL stored procedure that needs optimization. The procedure details are as follows:

database_type: {database_type}
procedure_purpose: {procedure_purpose}
performance_issue: {performance_issue}

Generate a basic optimized version of the stored procedure focusing on:
- Index usage
- Query structure
- Simple performance improvements
- Standard SQL patterns

Example:
database_type: "Microsoft SQL Server"
procedure_purpose: "Retrieves customer order history with filtering"
performance_issue: "Slow when filtering by date ranges on large tables"

Original Stored Procedure:
```sql
CREATE PROCEDURE GetCustomerOrderHistory
    @customer_id INT,
    @start_date DATE = NULL,
    @end_date DATE = NULL
AS
BEGIN
    SELECT 
        o.order_id,
        o.order_date,
        o.total_amount,
        p.product_name,
        od.quantity,
        od.unit_price
    FROM 
        Orders o
    JOIN 
        Order_Details od ON o.order_id = od.order_id
    JOIN 
        Products p ON od.product_id = p.product_id
    WHERE 
        o.customer_id = @customer_id
        AND (@start_date IS NULL OR o.order_date >= @start_date)
        AND (@end_date IS NULL OR o.order_date <= @end_date)
    ORDER BY 
        o.order_date DESC
END
```

Optimized Stored Procedure:
```sql
CREATE PROCEDURE GetCustomerOrderHistory
    @customer_id INT,
    @start_date DATE = NULL,
    @end_date DATE = NULL
AS
BEGIN
    -- Set nocount on to reduce network traffic
    SET NOCOUNT ON;
    
    -- Use table variables for smaller result sets, temp tables for larger ones
    DECLARE @filtered_orders TABLE (
        order_id INT PRIMARY KEY,
        order_date DATE,
        total_amount DECIMAL(10,2)
    );
    
    -- Filter orders in the first step to reduce joined data volume
    INSERT INTO @filtered_orders
    SELECT 
        order_id,
        order_date,
        total_amount
    FROM 
        Orders
    WHERE 
        customer_id = @customer_id
        AND (
            (@start_date IS NULL AND @end_date IS NULL) OR
            (@start_date IS NULL AND order_date <= @end_date) OR
            (@end_date IS NULL AND order_date >= @start_date) OR
            (order_date BETWEEN @start_date AND @end_date)
        );
    
    -- If no orders found, return early
    IF NOT EXISTS (SELECT 1 FROM @filtered_orders)
    BEGIN
        RETURN;
    END
    
    -- Join with the smaller filtered dataset
    SELECT 
        fo.order_id,
        fo.order_date,
        fo.total_amount,
        p.product_name,
        od.quantity,
        od.unit_price
    FROM 
        @filtered_orders fo
    JOIN 
        Order_Details od ON fo.order_id = od.order_id
    JOIN 
        Products p ON od.product_id = p.product_id
    ORDER BY 
        fo.order_date DESC
    OPTION (RECOMPILE); -- Helps with parameter sniffing issues
END
```

Recommended Indexes:
```sql
-- Add these indexes to improve performance
CREATE NONCLUSTERED INDEX IX_Orders_CustomerId_OrderDate
ON Orders (customer_id, order_date)
INCLUDE (total_amount);

CREATE NONCLUSTERED INDEX IX_OrderDetails_OrderId
ON Order_Details (order_id)
INCLUDE (product_id, quantity, unit_price);
```

Key points to consider:
1. Use appropriate indexing strategies for the query patterns
2. Filter data as early as possible to reduce join sizes
3. Use query hints sparingly and only when necessary
4. Structure queries for readability and maintainability
5. Consider database engine-specific optimizations but focus on standard techniques
```