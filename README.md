# Walmart Product Data Scraper

This project is a robust and scalable web scraper designed to extract detailed product information from Walmart’s online store. It systematically navigates Walmart’s search result pages for a wide range of technology and electronics-related products, gathering structured data and exporting it in JSON Lines (`.jsonl`) format.

## Objective

The primary goal of this scraper is to automate the collection of structured product data at scale from Walmart’s website for analytical, monitoring, or catalog-building purposes. It focuses on high-demand consumer electronics and related categories, enabling users to programmatically access pricing, availability, brand, rating, and product metadata.

## Extracted Product Information

For each product found through search queries, the scraper extracts:
- **Product name**
- **Brand**
- **Current price**
- **Availability status**
- **Short description**
- **Average customer rating**
- **Total number of reviews**
- **Item ID**
- **Thumbnail image URL**

## Key Features

- **Smart Search Querying**: Covers a comprehensive list of electronics-related keywords (e.g. `laptops`, `routers`, `cameras`, `xbox`, `modem`) to retrieve a wide product variety.
- **Pagination Handling**: Automatically iterates through paginated search results for each query, up to a predefined limit or until no more results are available.
- **URL Deduplication**: Ensures unique product URLs are processed only once using an in-memory `set`, improving efficiency and avoiding redundant data.
- **Structured HTML Parsing**: Utilizes BeautifulSoup to parse and navigate HTML and embedded JavaScript data structures reliably.
- **Retry Logic & Backoff Strategy**: Implements retry mechanisms with exponential backoff to handle transient HTTP failures, such as rate limits and timeouts.
- **Robust Error Logging**: Records failed URLs for both search pages and individual product pages, allowing for future reprocessing or debugging.
- **Randomized User-Agent Rotation**: Helps avoid detection and throttling by rotating through multiple realistic browser user-agent strings.
- **Modular, Clean Codebase**: Separation of concerns between search page scraping, product detail extraction, and data writing, improving readability and maintainability.

## Output

The scraper outputs the collected data to a file named `product_info.jsonl`, where each line is a standalone JSON object containing one product’s structured data. This format is ideal for downstream processing, transformation, or database ingestion.

### Sample Output (1 line per product):
```json
{
  "price": 299.99,
  "review_count": 134,
  "item_id": "781523942",
  "avg_rating": 4.3,
  "product_name": "HP 15.6\" Laptop",
  "brand": "HP",
  "availability": "InStock",
  "image_url": "https://i5.walmartimages.com/asr/xyz.jpg",
  "short_description": "Reliable laptop with AMD Ryzen processor..."
}
