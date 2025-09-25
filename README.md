# Real-time Collaborative Whiteboard

A modern, real-time collaborative whiteboard application built with Next.js 15, React, TypeScript, Tailwind CSS, and Yjs CRDT technology.

## Features

- 🎨 **Real-time Collaboration**: Multiple users can draw simultaneously with instant synchronization
- 🟦 **Shape Tools**: Draw rectangles and circles with click or drag interactions
- 🌐 **Room-based Sessions**: Create unique rooms and share links for collaboration
- ⚡ **CRDT Technology**: Conflict-free replicated data types ensure consistent state across all users
- 📱 **Responsive Design**: Beautiful, modern UI built with Tailwind CSS
- 🔄 **Automatic Sync**: Changes appear instantly across all connected devices
- 👥 **User Awareness**: See how many users are online in real-time

## Technology Stack

- **Frontend**: Next.js 15 (App Router), React 19, TypeScript
- **Backend**: Node.js WebSocket server
- **Real-time Sync**: Yjs CRDT library with WebSocket provider
- **Styling**: Tailwind CSS with modern gradients and animations
- **Build Tools**: TypeScript, ESLint, Prettier

## Getting Started

### Prerequisites

- Node.js 18+ 
- pnpm (recommended) or npm

### Installation

1. Clone the repository or navigate to the project directory
2. Install dependencies:
   ```bash
   pnpm install
   ```

### Development

Start both the frontend and WebSocket server simultaneously:

```bash
pnpm dev
```

This will start:
- Next.js frontend on `http://localhost:3000`
- WebSocket server on `ws://localhost:1234`

### Alternative: Start services separately

```bash
# Terminal 1: Start the WebSocket server
pnpm server

# Terminal 2: Start the frontend
pnpm dev:frontend
```

## Usage

1. **Create a Room**: Click "Create New Room" on the homepage to start a new collaborative session
2. **Join a Room**: Enter a room ID to join an existing session
3. **Draw Shapes**: 
   - Select Rectangle or Circle tool from the toolbar
   - Click to add shapes at default sizes
   - Drag to create custom-sized shapes
4. **Share**: Copy the room link to invite others to collaborate
5. **Collaborate**: Watch as other users' changes appear in real-time

## Project Structure

```
├── src/
│   ├── app/                    # Next.js App Router pages
│   │   ├── page.tsx           # Homepage with room creation/joining
│   │   └── room/[roomId]/     # Dynamic room pages
│   ├── components/            # React components
│   │   ├── WhiteboardCanvas.tsx  # SVG-based drawing canvas
│   │   ├── Toolbar.tsx        # Shape selection and tools
│   │   └── RoomHeader.tsx     # Room info and controls
│   ├── types/                 # TypeScript type definitions
│   │   └── whiteboard.ts      # Shape and state types
│   ├── utils/                 # Utility functions
│   │   └── yjsClient.ts       # Yjs document management
│   └── styles/               # Global styles
├── server/                   # WebSocket server
│   └── server.ts            # Yjs WebSocket integration
└── public/                  # Static assets
```

## Architecture

### Real-time Collaboration

The application uses **Yjs** (a CRDT library) for conflict-free collaborative editing:

1. **Document Sync**: Each room has a shared Yjs document containing a `shapes` array
2. **WebSocket Transport**: Changes are synchronized via WebSocket connections
3. **Automatic Merging**: Multiple users can edit simultaneously without conflicts
4. **Persistence**: Room state persists in memory (resets on server restart)

### Frontend Architecture

- **Next.js App Router**: Modern routing with React Server Components where applicable
- **Client-side State**: Room pages use client components for real-time interactions
- **SVG Rendering**: Shapes are rendered as SVG elements for crisp vector graphics
- **Responsive Design**: Mobile-friendly interface with Tailwind CSS

### Backend Architecture

- **Minimal Server**: Simple WebSocket server using the `ws` library
- **Yjs Integration**: `y-websocket/bin/utils` handles all CRDT synchronization
- **Room Isolation**: Each room URL path creates a separate document instance

## Building for Production

```bash
# Build the frontend
pnpm build

# Start production server
pnpm start

# Run WebSocket server (in another terminal)
pnpm server
```

## Customization

### Adding New Shape Types

1. Update `src/types/whiteboard.ts` with new shape interfaces
2. Add shape creation methods to `src/utils/yjsClient.ts`
3. Update rendering logic in `src/components/WhiteboardCanvas.tsx`
4. Add tool buttons to `src/components/Toolbar.tsx`

### Styling

The application uses Tailwind CSS for styling. Key design features:
- Gradient backgrounds and buttons
- Smooth transitions and hover effects
- Modern card-based layouts
- Consistent spacing and typography

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Run `pnpm check` to ensure code quality
5. Submit a pull request

## License

This project is open source and available under the MIT License.

## Acknowledgments

- **Yjs**: For providing excellent CRDT technology
- **Next.js**: For the modern React framework
- **Tailwind CSS**: For rapid UI development
- **WebSocket**: For real-time communication