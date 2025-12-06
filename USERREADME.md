# Star Citizen Organization Bot - User Guide

Welcome! This guide will help you use the Star Citizen Organization Discord Bot to manage your org's goals, inventory, and operations.

## What Can This Bot Do?

The bot helps your Star Citizen organization:
- 🎯 **Track Goals** - Set and monitor progress toward aUEC targets or specific items
- 📦 **Manage Inventory** - Keep track of ships, weapons, and other assets
- 📊 **Generate Reports** - Get weekly summaries of your org's progress
- 👥 **Manage Members** - Organize members with ranks and permissions

## Getting Started

### Permissions & Roles

The bot uses three permission levels:

- **👑 Officers** - Full access to all commands (create goals, manage inventory, configure bot)
- **📋 Logistics** - Can manage inventory and view member info
- **👤 Members** - Can view goals/inventory and update goal progress

Your server admins can configure which Discord roles have these permissions, or set them manually using bot commands.

---

## 🎯 Goal Management

### Creating Goals

There are two types of goals you can create:

#### 1. aUEC-Based Goals
Track progress toward a monetary target (e.g., "Save 10 million aUEC for a new ship").

**Command:** `/goal_create`
- **Name**: What you're working toward
- **Target Value**: How much aUEC you need
- **Category**: fleet, cargo, training, operations, pvp, exploration, mining, trading, other
- **Description**: (Optional) Additional details
- **Deadline**: (Optional) When you want to complete it (YYYY-MM-DD format)

**Example:**
```
/goal_create name:"Fleet Expansion Fund" target_value:50000000 category:fleet description:"Saving for 5 new Cutlass Blacks" deadline:2024-12-31
```

#### 2. Item-Based Goals
Track progress toward collecting specific items (e.g., "Get 3 Cutlass Blacks and 10 AR-15s").

**Command:** `/goal_create_items`
- **Name**: What you're working toward
- **Category**: Same categories as above
- **Items**: List of required items in format `ItemName:Type:Quantity`
  - Separate multiple items with commas
  - Example: `Cutlass Black:ship:3,AR-15:weapon:10`
- **Description**: (Optional) Additional details
- **Deadline**: (Optional) When you want to complete it

**Example:**
```
/goal_create_items name:"Combat Fleet Ready" category:fleet items:"Cutlass Black:ship:3,Arrow:ship:5,AR-15:weapon:20" description:"Building our PvP fleet"
```

### Viewing Goals

**List all goals:** `/goal_list`
- Filter by category (optional)
- Show only active goals (default: yes)

**View specific goal:** `/goal_view`
- Enter the goal ID (shown when you create or list goals)

### Updating Progress

**For aUEC goals:** `/goal_update`
- Enter the goal ID
- Add or subtract aUEC (use negative numbers to subtract)
- Example: `/goal_update goal_id:5 delta:1000000` (adds 1M aUEC)

**For item-based goals:** `/goal_sync_items`
- Automatically syncs with your current inventory
- The bot checks what items you have and updates progress automatically

### Managing Goals

**Mark complete/incomplete:** `/goal_complete` (Officers only)
- Toggle a goal's active status
- Completed goals can be reactivated if needed

---

## 📦 Inventory Management

### Adding Items

**Command:** `/inv_add` (Logistics only)

**Required:**
- **Name**: Item name (e.g., "Cutlass Black", "AR-15")
- **Type**: ship, vehicle, weapon, armor, cargo, component, consumable, other

**Optional:**
- **Quantity**: How many (default: 1)
- **Location**: Where it's stored
- **Notes**: Additional information
- **Owner ID**: Discord ID if owned by a member (leave empty for org-owned)

**Example:**
```
/inv_add name:"Cutlass Black" type:ship quantity:2 location:"Hangar 3" notes:"Fully upgraded"
```

### Viewing Inventory

**List items:** `/inv_list`
- Filter by type (optional)
- Filter by owner Discord ID (optional)

**Search by name:** `/inv_find`
- Type part of the item name to search
- Example: `/inv_find query:"Cutlass"` finds all items with "Cutlass" in the name

**View specific item:** `/inv_view`
- Enter the item ID (shown when you add or list items)

### Updating Inventory

**Update item:** `/inv_update` (Logistics only)
- Change quantity, location, or notes
- Only update the fields you want to change

**Remove item:** `/inv_remove` (Logistics only)
- Permanently removes an item from inventory

---

## 📊 Reports

### Manual Reports

**Command:** `/report_generate` (Officers only)

Generates a summary showing:
- Active goals and progress
- Inventory totals by type
- Member count
- Overall statistics

### Automatic Weekly Reports

Your server admins can configure the bot to automatically post weekly reports to a specific channel. These reports include:
- Goals summary with top performers
- Inventory breakdown
- Member statistics

Contact your server admins to set up automatic reports.

---

## 👥 Member Management

### Setting Member Ranks

**Command:** `/admin_member_set_rank` (Officers only)

Set a member's organization rank:
- **member** - Basic access
- **logistics** - Can manage inventory
- **officer** - Full access
- **admin** - Full access (highest level)

**Example:**
```
/admin_member_set_rank member_id:123456789012345678 rank:logistics
```

### Viewing Member Info

**Command:** `/admin_member_info` (Officers only)

Shows:
- Member's rank
- Join date
- Number of goals created
- Number of inventory items owned

---

## ⚙️ Server Configuration

These commands help admins configure the bot for your server.

### Setting Roles

**Command:** `/admin_config_set_role` (Officers only)

Configure which Discord roles have permissions:
- Set the **officer** role (full access)
- Set the **logistics** role (inventory management)
- Leave empty to clear/remove a role

### Report Settings

**Set report channel:** `/admin_config_set_report_channel` (Officers only)
- Choose which channel receives weekly reports
- Leave empty to disable automatic reports

**Set report schedule:** `/admin_config_set_report_time` (Officers only)
- **Day**: 0 = Monday, 1 = Tuesday, ..., 6 = Sunday
- **Hour**: 0-23 in UTC (24-hour format)
- Example: `/admin_config_set_report_time day:0 hour:9` (Monday at 9 AM UTC)

### View Configuration

**Command:** `/admin_config_view` (Officers only)

Shows all current server settings:
- Officer and Logistics roles
- Report channel
- Report schedule

---

## 💡 Tips & Examples

### Example Workflow: Setting Up a Fleet Goal

1. **Create an item-based goal:**
   ```
   /goal_create_items name:"Fleet Expansion" category:fleet items:"Cutlass Black:ship:5,Arrow:ship:10"
   ```

2. **Add ships to inventory as you acquire them:**
   ```
   /inv_add name:"Cutlass Black" type:ship quantity:1 location:"Hangar 1"
   ```

3. **Sync the goal to update progress:**
   ```
   /goal_sync_items goal_id:1
   ```

4. **View progress anytime:**
   ```
   /goal_view goal_id:1
   ```

### Example Workflow: Tracking aUEC Savings

1. **Create an aUEC goal:**
   ```
   /goal_create name:"Capital Ship Fund" target_value:100000000 category:fleet deadline:2024-12-31
   ```

2. **Update progress as members contribute:**
   ```
   /goal_update goal_id:2 delta:5000000
   ```

3. **Check progress:**
   ```
   /goal_list active_only:True
   ```

### Finding Items

Use `/inv_find` to quickly locate items:
- `/inv_find query:"weapon"` - Find all weapons
- `/inv_find query:"Cutlass"` - Find all Cutlass variants
- `/inv_find query:"AR"` - Find AR-series weapons

---

## ❓ Common Questions

**Q: Why can't I use a command?**
A: Check your permissions. Officers have full access, Logistics can manage inventory, and Members can view and update goals.

**Q: How do I find a goal or item ID?**
A: IDs are shown when you create items/goals, or when you use `/goal_list` or `/inv_list`.

**Q: Can I delete a goal?**
A: Use `/goal_complete` to mark it inactive. Goals are kept for historical records.

**Q: How do item-based goals work?**
A: They automatically check your inventory for matching items (by name and type). Use `/goal_sync_items` to update progress.

**Q: What's the difference between org-owned and member-owned items?**
A: Org-owned items belong to the organization. Member-owned items are tracked to a specific Discord user. Both count toward item-based goals.

**Q: How do I set up weekly reports?**
A: Officers can use `/admin_config_set_report_channel` and `/admin_config_set_report_time` to configure automatic reports.

---

## 🎮 Quick Reference

### Goal Commands
- `/goal_create` - Create aUEC goal (Officers)
- `/goal_create_items` - Create item goal (Officers)
- `/goal_list` - List goals
- `/goal_view` - View goal details
- `/goal_update` - Update aUEC progress (Members)
- `/goal_sync_items` - Sync item goal (Members)
- `/goal_complete` - Toggle goal status (Officers)

### Inventory Commands
- `/inv_add` - Add item (Logistics)
- `/inv_list` - List items
- `/inv_find` - Search items
- `/inv_view` - View item details
- `/inv_update` - Update item (Logistics)
- `/inv_remove` - Remove item (Logistics)

### Admin Commands
- `/admin_member_set_rank` - Set member rank (Officers)
- `/admin_member_info` - View member info (Officers)
- `/admin_config_set_role` - Configure roles (Officers)
- `/admin_config_set_report_channel` - Set report channel (Officers)
- `/admin_config_set_report_time` - Set report schedule (Officers)
- `/admin_config_view` - View configuration (Officers)
- `/report_generate` - Generate report (Officers)

---

## 📝 Notes

- All dates use UTC timezone
- Item names are case-insensitive when syncing goals
- Goals can be filtered by category using autocomplete
- The bot supports multiple Discord servers with separate data
- Discord administrators always have full access

---

**Need Help?** Contact your server administrators or open an issue on the bot's repository.

**Happy Organizing!** 🚀

