# Super Field - Network

A specialized network address input component for Budibase applications with IP address validation, CIDR notation support, and network range handling.

## 🚀 Features

### Network Input

- **IP Address Support**: IPv4 and IPv6 address validation
- **CIDR Notation**: Network range specification with subnet masks
- **Range Calculation**: Automatic network range computation
- **Address Validation**: Format validation for network addresses
- **Default Values**: Pre-configured network addresses

### Data Handling

- **String Field Binding**: Standard string field integration
- **Range Context**: Network range information in component context
- **Template Formatting**: Custom network address display
- **Event Handling**: On change events with network context
- **State Management**: Disabled and readonly modes

### User Experience

- **Input Validation**: Real-time network address validation
- **Help Text**: Guidance for network address formats
- **Auto-completion**: Network address suggestions
- **Error Feedback**: Clear validation error messages
- **Debounced Input**: Performance optimization for network lookups

### Advanced Features

- **CIDR Support**: Classless Inter-Domain Routing notation
- **Subnet Calculation**: Automatic subnet mask handling
- **Network Analysis**: IP range and subnet information
- **Integration**: Network device and infrastructure management
- **Conditional Logic**: Dynamic behavior based on network values

### Styling & Layout

- **Flexible Positioning**: Label placement options
- **Field Modes**: Form input or inline editing
- **Size Configuration**: Adjustable component width
- **Theme Integration**: Consistent with Budibase design

## 📝 Usage Instructions

### Basic Setup

1. Add the Super Field - Network component to your form
2. Bind to a string field for storing network addresses
3. Configure validation for IP address formats
4. Set help text for network address requirements

### Advanced Configuration

- **CIDR Support**: Enable CIDR notation for network ranges
- **Validation**: Configure IP address and network validation
- **Range Display**: Show calculated network ranges
- **Events**: Attach actions to network address changes

### Common Use Cases

- **Network Configuration**: IP address management
- **Firewall Rules**: Network access control lists
- **VPN Setup**: Virtual private network configuration
- **Infrastructure Management**: Server and device IP assignment
- **Security Policies**: Network security rule definition

## 🔧 Configuration Options

| Setting          | Type     | Description                   |
| ---------------- | -------- | ----------------------------- |
| Field            | String   | Network address field binding |
| Label            | String   | Display label text            |
| Placeholder      | String   | Input guidance text           |
| Default Value    | String   | Pre-set network address       |
| Formatted Value  | Template | Network display formatting    |
| Help Text        | String   | Help/instruction text         |
| Validation       | Rules    | Network address validation    |
| Debounced        | Boolean  | Enable input debouncing       |
| Disabled         | Boolean  | Disable network input         |
| Read Only        | Boolean  | Read-only mode                |
| Clear Value Icon | Boolean  | Show clear icon button        |
| Icon             | Icon     | Visual indicator icon         |
| Field Mode       | Select   | Form or inline input style    |
| Label Position   | Select   | Label placement               |
| Size             | Number   | Component width span          |

## 📋 Events

### On Change

Triggered when network address changes.

**Context:**

- `value`: Current network address value
- `range`: Calculated network range information
- `field`: The bound field information

## 🎨 Styling

The component supports Budibase's styling system with:

- **Network Formatting**: Clear IP address display
- **Validation States**: Error highlighting for invalid addresses
- **Icon Integration**: Network-related visual indicators
- **Responsive**: Mobile-friendly network input

## 🔍 Best Practices

- Specify expected IP address formats in help text
- Use CIDR notation for network range specifications
- Implement validation for network address requirements
- Consider debouncing for network lookups
- Test with various IP address formats
- Provide clear network configuration guidance
