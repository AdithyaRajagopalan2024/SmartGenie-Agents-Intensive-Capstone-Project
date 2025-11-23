# ShopGenie - AI Shopping Assistant

## Overview
ShopGenie is a multi-agent AI shopping assistant built with Google ADK that helps users:
- Search for products by category, price, brand, color, and features
- Place and manage orders
- Track order status and handle returns

## Architecture

### Multi-Agent System
1. **Orchestrator Agent**: Routes user requests and coordinates sub-agents
2. **Product Agent**: Handles product search and recommendations
3. **Service Agent**: Manages orders, returns, and customer service

### Key Features
- Natural language product search
- Intent parsing with fuzzy matching
- SQL database for product/order management
- Multi-turn conversation support
- Error handling for out-of-stock and invalid requests
- Memory service for user preferences

## Tech Stack
- **Framework**: Google Agent Development Kit (ADK)
- **LLM**: Gemini 2.5 Flash Lite
- **Database**: SQLAlchemy + SQLite
- **Tools**: Custom Python functions for product/order operations

## Setup

### Prerequisites
```bash
pip install google-adk google-genai sqlalchemy aiosqlite
```

### Environment Variables
```bash
export GOOGLE_API_KEY="your-api-key-here"
```

### Running
```python
import asyncio
from agent import runner

# Single query
events = await runner.run_debug(
    "Show me black running shoes under 3500",
    user_id="user123",
    session_id="session123"
)
```

## Example Interactions

### Product Search
```
User: "Show me black running shoes under 3500"
Agent: "I found 1 black running shoes under 3500.

**Nike Revolution 6**
* Price: 2799
* Features: Cushioned, breathable, lightweight, durable
* Stock: 12 available"
```

### Order Placement
```
User: "Order 2 units of product 1"
Agent: "Great! I've placed your order:
- Order ID: 1
- Product: Nike Revolution 6
- Quantity: 2
- Total: ₹5,598"
```

### Error Handling
```
User: "Order 100 units of product 1"
Agent: "I'm sorry, we only have 12 units of Nike Revolution 6 in stock."
```

## Database Schema

### Products Table
- id (Primary Key)
- name, category, brand
- price, color
- features (JSON)
- rating, stock

### Orders Table
- order_id (Primary Key)
- product_id, product
- quantity, total_price

## Evaluation
The agent is tested against:
- Product search accuracy
- Order placement success
- Error handling for edge cases
- Multi-turn conversations

## Future Enhancements
- [ ] Add recommendation engine
- [ ] Implement cart management
- [ ] Add payment integration
- [ ] Support multiple languages
- [ ] Add product reviews and ratings
