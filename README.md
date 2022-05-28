# Maven-Fuzzy-E-commerce-Analysis

## Session-1 E-Commerce Traffic Source Analysis
## 1. Use the UTM parameters stored in the database to identify paid website sessions 
## 2. From the session data, link it to the order data -> to understand how much revenue the paid campaigns are driving 

## Needed SQL: GROUP BY, COUNT(), SUM 
## Code Below :

SELECT
     website_sessions.utm_source,
     website_sessions.utm_campaign,
     website_sessions.utm_content,
     COUNT(DISTINCT website_sessions.website_session_id) as sessions,
     COUNT(DISTINCT orders.order_id) as ordersnum,
     (COUNT(DISTINCT orders.order_id)/COUNT(DISTINCT website_sessions.website_session_id))*100 AS prct_session_to_order_conv_rt
  FROM 
     website_sessions
  LEFT JOIN orders 
    ON website_sessions.user_id = orders.user_id
    
 WHERE 
     website_sessions.website_session_id BETWEEN 1000 AND 2000
     
 GROUP BY 3
 ORDER BY 4 DESC
