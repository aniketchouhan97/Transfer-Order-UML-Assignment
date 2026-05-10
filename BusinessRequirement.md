# FMCG Transfer Order Management - Requirements

## 1. Business Requirement
- The business operates in the Fast-Moving Consumer Goods (FMCG) segment with multiple stores (e.g., 10 stores) spread nationwide across different states.
- The business utilizes a large stock and warehouse model. Each store may have its own dedicated warehouse, which can be located at the same physical location as the store or separated by some distance.
- There is a daily need to identify material shortages across all store locations.
- When a store experiences a shortage, the system must facilitate the transfer of stock from other eligible stores or warehouses to meet the demand.
- Given the FMCG nature of the products, items have expiration dates that must be strictly managed during transfers to minimize spoilage and adhere to safety standards.

## 2. Objective
- **Visibility & Identification:** Provide a system that automatically identifies daily material shortages at each store location based on predefined threshold levels.
- **Transfer Enablement:** Empower warehouse managers to seamlessly initiate and manage material transfers between eligible locations.
- **Expiry Management:** Optimize inventory movement by prioritizing the transfer of items with earlier expiration dates (FEFO - First Expiring, First Out).
- **Data Integrity:** Ensure that critical item attributes, specifically Lot Numbers and Expiry Dates, are retained and accurately tracked throughout the entire shipment and receiving process.
- **Future Promising:** Provide visibility into in-transit shipments so that the destination store/warehouse can promise future customer orders against the incoming transfer stock before it physically arrives.

## 3. Transfer Order Logic
- **Shortage Identification (Receiving Eligibility):**
  - A store (and its attached warehouse) is flagged for material shortages and becomes eligible to *receive* transfers if its total stock position falls below **20% above the buffer level** (i.e., Total Stock < Buffer Level + 20%).
- **Sender Eligibility Criteria:**
  - To determine which store/warehouse is eligible to *transfer out* material to a demanding store, the system evaluates two primary factors:
    1. **Inventory Turnover Ratio:** The sender location must have a suitable inventory turnover ratio to ensure they are not prematurely depleted of items they sell quickly.
    2. **Zonal Restrictions:** Transfers are restricted to within the same geographical zone (e.g., East Coast locations can only transfer to other East Coast locations; West Coast to West Coast).
- **Inventory Selection & Expiry Logic (FEFO):**
  - When preparing a shipment, the user can cherry-pick specific items to ship.
  - The system must actively suggest inventory to ship out based on expiry dates, ensuring items expiring sooner are pushed out ahead of later expiry dates.
- **Shipment Processing ("Pick Pack and Ship"):**
  - Transfer shipments bypass complex standard fulfillment routing. They follow a straightforward "Pick Pack and Ship" process where items are directly picked, packed, and shipped out because the exact quantity and destination are known.
- **Receiving & Attribute Inheritance:**
  - Upon receiving the transfer at the destination warehouse, all identifiers from the origin must be inherited. The system must retain the exact Lot Numbers and Expiry Dates tied to the received inventory.
- **In-Transit Order Promising:**
  - The destination warehouse must have visibility into the incoming transfer volume (intrinsic stock). The system must allow customer orders to be promised against this incoming stock before it is physically received and marked as available.

## 4. Activity Diagram

[Activity Diagram](./Activity_Diagram.png)

![alt text](image-1.png)
