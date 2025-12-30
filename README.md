# Ace Ticket iOS App

![Ace Ticket Logo](https://img.shields.io/badge/Ace%20Ticket-Official%20iOS%20App-blue.svg)
![iOS](https://img.shields.io/badge/iOS-13%2B-green.svg)
![Swift](https://img.shields.io/badge/Swift-5.0-orange.svg)
![License](https://img.shields.io/badge/License-MIT-lightgrey.svg)

Boston's premier ticketing app for sports, concerts, and entertainment events.

## 🎟️ Overview

Ace Ticket iOS is a comprehensive ticketing application designed for Boston-area events. The app provides a seamless experience for browsing, purchasing, and managing tickets for:

- **Sports**: MLB (Red Sox), NHL (Bruins), NBA (Celtics), NFL (Patriots), NCAA (BC, Harvard)
- **Concerts**: Major artists and venues across Boston
- **Theater**: Broadway shows and local productions
- **Festivals**: Boston Calling and other major events
- **Other**: Comedy shows, wrestling, MMA, golf, tennis, and racing

## 🚀 Features

### 📱 Core Functionality
- **Event Browsing**: Browse 35+ realistic Boston events across 16 categories
- **Search & Filter**: Advanced filtering by category, date, venue, and team/artist
- **Favorites**: Save your favorite events for quick access
- **Calendar Integration**: Add events to your device calendar
- **Map Integration**: View Boston venue locations

### 🎫 Ticket Management
- **My Tickets**: View all your purchased tickets in one place
- **QR Code Display**: Scan-ready QR codes for all tickets
- **Seat Information**: Detailed seat location (section, row, seat)
- **Ticket Status**: Track ticket status (Active, Used, Expired, Refunded)
- **Ticket Sharing**: Share tickets with friends

### 🎨 User Experience
- **Modern Design**: Clean, professional interface with Ace Ticket branding
- **Offline Support**: Browse events without internet connection
- **Empty States**: Helpful messaging and clear calls-to-action
- **Responsive Design**: Optimized for all iPhone sizes

## 🏗️ Architecture

### MVVM Pattern
The app follows the Model-View-ViewModel (MVVM) pattern with Protocol-Oriented Programming:

```
┌─────────────────────────────────────────────────────────────────────┐
│                         PRESENTATION LAYER                          │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐  │
│  │  ViewControllers │  │    Storyboards   │  │      Cells       │  │
│  │  (9 storyboards) │  │   (9 .storyboard)│  │   (EventCell)    │  │
│  └──────────────────┘  └──────────────────┘  └──────────────────┘  │
│           │                                                         │
│           ▼                                                         │
│  ┌──────────────────────────────────────────────────────────────┐  │
│  │                      VIEWMODEL LAYER                          │  │
│  │  EventViewModel │ ScheduleViewModel │ EventsListViewModel    │  │
│  │  TrackViewModel │ SpeakerViewModel                           │  │
│  │  (Observable<T> for reactive binding)                        │  │
│  └────────┬─────────────────────────────────────────────────────┘  │
│           │                                                         │
└───────────┼─────────────────────────────────────────────────────────┘
            │
┌───────────┼─────────────────────────────────────────────────────────┐
│           ▼                    DATA LAYER                           │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐  │
│  │   EventProvider  │  │  FetchDataService│  │  SettingsManager │  │
│  │ (business logic) │  │ (data fetching)  │  │  (UserDefaults)  │  │
│  └────────┬─────────┘  └────────┬─────────┘  └──────────────────┘  │
│           │                     │                                   │
│           ▼                     ▼                                   │
│  ┌──────────────────┐  ┌──────────────────┐                        │
│  │    ApiClient     │  │     Client       │                        │
│  │ (URLSession-JSON)│  │ (Alamofire-Auth) │                        │
│  └────────┬─────────┘  └────────┬─────────┘                        │
│           │                     │                                   │
└───────────┼─────────────────────┼───────────────────────────────────┘
            │                     │
            ▼                     ▼
   GitHub Raw JSON         Open Event API
   (Events Data)           (Auth Only)
```

### Key Technologies
- **Swift 5.0+**: Modern Swift with protocol-oriented design
- **UIKit**: Native iOS interface components
- **MVVM Architecture**: Clean separation of concerns
- **Observable Pattern**: Reactive data binding
- **CoreImage**: QR code generation
- **MapKit**: Venue location mapping
- **Alamofire**: HTTP networking (ready for API integration)

## 📦 Installation

### Prerequisites
- Xcode 12.0+
- iOS 13.0+
- CocoaPods 1.10.0+

### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/acg-data/AceTix_iOS.git
   cd AceTix_iOS
   ```

2. Install dependencies:
   ```bash
   pod install
   ```

3. Open the workspace:
   ```bash
   open FOSSAsia.xcworkspace
   ```

4. Build and run in Xcode

## 🎨 Branding

### Color Palette
- **Primary Blue**: #1565C0 (Brand color)
- **Light Blue**: #E3F2FD (Highlights)
- **White**: #FFFFFF (Backgrounds)
- **Dark Gray**: #212121 (Primary text)
- **Medium Gray**: #757575 (Secondary text)
- **Orange**: #FF6F00 (Favorites/Actions)

### Typography
- **Headings**: System Bold (17-24pt)
- **Body**: System Regular/Medium (14-16pt)
- **Labels**: System Regular (12-14pt)

## 📱 Screenshots

[Add screenshots here when available]

## 🔧 Configuration

### Constants
Update `Constants.swift` for your environment:
```swift
struct Constants {
    struct Url {
        static let aceTicketAPI = "https://api.aceticket.com/v1"
        static let eventsEndpoint = "https://api.aceticket.com/v1/events"
        static let ticketsEndpoint = "https://api.aceticket.com/v1/tickets"
        static let venuesEndpoint = "https://api.aceticket.com/v1/venues"
    }
}
```

### Assets
Replace placeholder assets in `Assets.xcassets/`:
- App icon (1024x1024)
- Launch screen logo
- Tab bar icons
- Event placeholder images

## 🚀 Development

### Adding New Event Categories
1. Update `Event.swift` Track enum
2. Add corresponding color in `Event.Track.getTrackColor()`
3. Update `DummyData/sessions.json` with new events
4. Test in app

### Adding Real API Integration
1. Update `Constants.swift` with real API endpoints
2. Modify `MockDataService.swift` to use real API calls
3. Update `ApiClient.swift` for new endpoints
4. Test authentication flow

### Adding Payment Integration
1. Integrate with payment provider (Stripe, Braintree, etc.)
2. Update `TicketDetailViewController.swift` with payment UI
3. Add payment processing in `TicketService.swift`
4. Update models for transaction data

## 🧪 Testing

### Unit Tests
```bash
# Run tests in Xcode
Product > Test (⌘+U)
```

### UI Tests
```bash
# Run UI tests
Product > Test (⌘+U) with UI tests scheme
```

### Manual Testing Checklist
- [ ] App launches without crashes
- [ ] Browse tab shows events
- [ ] Favorites add/remove works
- [ ] My Tickets displays sample tickets
- [ ] QR codes generate and display
- [ ] Navigation flows work
- [ ] Map shows Boston location
- [ ] Profile updates work
- [ ] More links open in Safari

## 📊 Analytics & Monitoring

### Ready for Integration
The app is structured to easily add:
- **Firebase Analytics**: User behavior tracking
- **Crashlytics**: Error monitoring
- **Performance Monitoring**: App performance metrics

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Original FOSSASIA Open Event iOS**: Base codebase and architecture
- **Boston Sports & Entertainment**: Inspiration for event categories
- **iOS Community**: Frameworks and libraries used

## 📞 Support

For support and questions:
- Create an issue in this repository
- Contact the development team
- Check the [documentation](docs/)

---

**Built with ❤️ for Boston's sports and entertainment fans**