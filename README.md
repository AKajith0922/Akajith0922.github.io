



### ASSISTANT
```jsx
import React, { useState, useEffect } from "react";

export default function App() {
  const [currentPage, setCurrentPage] = useState("home");
  const [searchQuery, setSearchQuery] = useState("");
  const [isDarkMode, setIsDarkMode] = useState(true);
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  const [activeVideo, setActiveVideo] = useState(null);

  // Mock data for videos
  const videoCategories = {
    trending: [
      { id: 1, title: "Solar Flares in Action", category: "Science", thumbnail: "https://picsum.photos/400/225?random=1" },
      { id: 2, title: "Fusion Energy Breakthrough", category: "Tech", thumbnail: "https://picsum.photos/400/225?random=2" },
      { id: 3, title: "Future of Space Travel", category: "Space", thumbnail: "https://picsum.photos/400/225?random=3" },
      { id: 4, title: "Sunext: The Solar Revolution", category: "Documentary", thumbnail: "https://picsum.photos/400/225?random=4" },
      { id: 5, title: "The Power of Light", category: "Science", thumbnail: "https://picsum.photos/400/225?random=5" },
      { id: 6, title: "Energy of Tomorrow", category: "Tech", thumbnail: "https://picsum.photos/400/225?random=6" },
    ],
    popular: [
      { id: 7, title: "Quantum Computing and Light", category: "Tech", thumbnail: "https://picsum.photos/400/225?random=7" },
      { id: 8, title: "Sustainable Cities", category: "Environment", thumbnail: "https://picsum.photos/400/225?random=8" },
      { id: 9, title: "Solar Innovations", category: "Science", thumbnail: "https://picsum.photos/400/225?random=9" },
      { id: 10, title: "Light Speed Travel", category: "Space", thumbnail: "https://picsum.photos/400/225?random=10" },
    ],
  };

  const filteredVideos = Object.entries(videoCategories).reduce((acc, [key, videos]) => {
    acc[key] = videos.filter(
      (video) =>
        video.title.toLowerCase().includes(searchQuery.toLowerCase()) ||
        video.category.toLowerCase().includes(searchQuery.toLowerCase())
    );
    return acc;
  }, {});

  const handleLogin = () => {
    setIsLoggedIn(true);
    setCurrentPage("home");
  };

  const handleLogout = () => {
    setIsLoggedIn(false);
  };

  const openVideoPlayer = (video) => {
    setActiveVideo(video);
    setCurrentPage("player");
  };

  const renderLogo = () => (
    <div className="flex items-center space-x-2">
      <svg viewBox="0 0 50 50" width="30" height="30" className="text-orange-400">
        <circle cx="25" cy="25" r="20" fill="currentColor" />
        <path
          d="M25 5v10M25 35v10M10.6 10.6l7.07 7.07m5.66 5.66a15 15 0 1 0 0-21.22"
          stroke="white"
          strokeWidth="2"
          fill="none"
        />
      </svg>
      <span className="text-xl font-bold text-white">FANALTIC</span>
    </div>
  );

  const renderNav = () => (
    <nav className="hidden md:flex space-x-6 text-sm font-medium">
      <button onClick={() => setCurrentPage("home")} className="hover:text-orange-400 transition-colors">
        Home
      </button>
      <button onClick={() => setCurrentPage("browse")} className="hover:text-orange-400 transition-colors">
        Browse
      </button>
      {isLoggedIn && (
        <button onClick={() => setCurrentPage("profile")} className="hover:text-orange-400 transition-colors">
          Profile
        </button>
      )}
    </nav>
  );

  const renderMobileNav = () => (
    <div className="md:hidden flex justify-between items-center w-full mt-4">
      <button onClick={() => setCurrentPage("home")} className="text-white hover:text-orange-400">
        Home
      </button>
      <button onClick={() => setCurrentPage("browse")} className="text-white hover:text-orange-400">
        Browse
      </button>
      {isLoggedIn ? (
        <button onClick={handleLogout} className="text-white hover:text-orange-400">
          Logout
        </button>
      ) : (
        <button onClick={() => setCurrentPage("login")} className="text-white hover:text-orange-400">
          Login
        </button>
      )}
    </div>
  );

  const renderHero = () => (
    <section className="relative h-screen flex flex-col justify-center items-center text-center px-4 overflow-hidden">
      <div className="absolute inset-0 bg-gradient-to-br from-orange-500 via-yellow-300 to-purple-900 opacity-30 blur-lg"></div>
      <div className="z-10 max-w-3xl">
        <h1 className="text-4xl sm:text-6xl font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-orange-400 via-yellow-300 to-white mb-4">
          Stream the Future of Video
        </h1>
        <p className="text-lg sm:text-xl text-gray-200 mb-8">
          Explore solar-powered content, futuristic visuals, and the energy of tomorrow.
        </p>
        <button
          onClick={() => setCurrentPage("browse")}
          className="px-6 py-3 bg-gradient-to-r from-orange-500 to-yellow-400 text-black rounded-full font-semibold shadow-lg hover:shadow-xl transform hover:-translate-y-1 transition-all duration-300"
        >
          Start Browsing
        </button>
      </div>
    </section>
  );

  const renderBrowseSection = () => (
    <section className="py-12 px-4">
      <div className="max-w-6xl mx-auto">
        <h2 className="text-3xl font-bold text-white mb-8">Trending Videos</h2>
        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 mb-12">
          {filteredVideos.trending.map((video) => (
            <div
              key={video.id}
              onClick={() => openVideoPlayer(video)}
              className="bg-white/5 backdrop-blur-md rounded-xl overflow-hidden border border-white/10 hover:border-orange-400 transition-all cursor-pointer group"
            >
              <div className="relative">
                <img src={video.thumbnail} alt={video.title} className="w-full h-40 object-cover" />
                <div className="absolute inset-0 bg-gradient-to-t from-black/70 to-transparent opacity-0 group-hover:opacity-100 transition-opacity flex items-end p-4">
                  <span className="text-xs font-semibold bg-orange-500 text-white px-2 py-1 rounded-full">{video.category}</span>
                </div>
              </div>
              <div className="p-4">
                <h3 className="font-semibold text-white text-lg">{video.title}</h3>
              </div>
            </div>
          ))}
        </div>

        <h2 className="text-3xl font-bold text-white mb-8">Popular</h2>
        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
          {filteredVideos.popular.map((video) => (
            <div
              key={video.id}
              onClick={() => openVideoPlayer(video)}
              className="bg-white/5 backdrop-blur-md rounded-xl overflow-hidden border border-white/10 hover:border-orange-400 transition-all cursor-pointer group"
            >
              <div className="relative">
                <img src={video.thumbnail} alt={video.title} className="w-full h-40 object-cover" />
                <div className="absolute inset-0 bg-gradient-to-t from-black/70 to-transparent opacity-0 group-hover:opacity-100 transition-opacity flex items-end p-4">
                  <span className="text-xs font-semibold bg-orange-500 text-white px-2 py-1 rounded-full">{video.category}</span>
                </div>
              </div>
              <div className="p-4">
                <h3 className="font-semibold text-white text-lg">{video.title}</h3>
              </div>
            </div>
          ))}
        </div>
      </div>
    </section>
  );

  const renderSearchBar = () => (
    <div className="mb-10 relative">
      <input
        type="text"
        placeholder="Search videos or categories..."
        value={searchQuery}
        onChange={(e) => setSearchQuery(e.target.value)}
        className="w-full px-6 py-3 rounded-full bg-white/10 border border-white/20 text-white placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-orange-400 backdrop-blur-md"
      />
      <svg
        className="absolute right-4 top-1/2 transform -translate-y-1/2 w-5 h-5 text-gray-400"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
      </svg>
    </div>
  );

  const renderVideoPlayer = () => (
    <section className="py-12 px-4 min-h-screen">
      <div className="max-w-5xl mx-auto">
        <div className="aspect-video bg-black rounded-xl mb-6 overflow-hidden shadow-2xl">
          <video controls className="w-full h-full object-cover">
            <source src="https://www.w3schools.com/html/mov_bbb.mp4" type="video/mp4" />
            Your browser does not support the video tag.
          </video>
        </div>

        <h2 className="text-2xl font-bold text-white mb-2">{activeVideo?.title}</h2>
        <p className="text-gray-400 mb-6">Category: {activeVideo?.category}</p>

        <div className="grid grid-cols-1 lg:grid-cols-3 gap-8">
          <div className="lg:col-span-2">
            <h3 className="text-xl font-semibold text-white mb-4">Comments</h3>
            <div className="space-y-4">
              <div className="bg-white/5 p-4 rounded-lg">
                <div className="flex items-center mb-2">
                  <div className="w-8 h-8 rounded-full bg-orange-400 mr-3"></div>
                  <span className="text-white font-medium">User123</span>
                </div>
                <p className="text-gray-300">This is an amazing look into the future of energy!</p>
              </div>
              <div className="bg-white/5 p-4 rounded-lg">
                <div className="flex items-center mb-2">
                  <div className="w-8 h-8 rounded-full bg-yellow-400 mr-3"></div>
                  <span className="text-white font-medium">ScienceEnthusiast</span>
                </div>
                <p className="text-gray-300">Love how they blend tech with environmental consciousness.</p>
              </div>
            </div>
          </div>

          <div>
            <h3 className="text-xl font-semibold text-white mb-4">Recommendations</h3>
            <div className="space-y-4">
              {videoCategories.trending.slice(0, 3).map((video) => (
                <div
                  key={video.id}
                  onClick={() => openVideoPlayer(video)}
                  className="flex items-center space-x-3 cursor-pointer hover:bg-white/5 p-2 rounded-lg transition-colors"
                >
                  <img src={video.thumbnail} alt={video.title} className="w-16 h-10 rounded object-cover" />
                  <div>
                    <p className="text-white font-medium text-sm">{video.title}</p>
                    <p className="text-gray-400 text-xs">{video.category}</p>
                  </div>
                </div>
              ))}
            </div>
          </div>
        </div>
      </div>
    </section>
  );

  const renderLogin = () => (
    <section className="py-12 px-4 min-h-screen flex items-center justify-center">
      <div className="max-w-md w-full bg-white/5 backdrop-blur-md p-8 rounded-2xl border border-white/10 shadow-xl">
        <h2 className="text-2xl font-bold text-white mb-6 text-center">Welcome to FANALTIC</h2>
        <form className="space-y-4">
          <div>
            <label htmlFor="email" className="block text-sm font-medium text-gray-300 mb-1">
              Email
            </label>
            <input
              type="email"
              id="email"
              className="w-full px-4 py-2 bg-white/10 border border-white/20 rounded-lg text-white placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-orange-400"
              placeholder="you@example.com"
            />
          </div>
          <div>
            <label htmlFor="password" className="block text-sm font-medium text-gray-300 mb-1">
              Password
            </label>
            <input
              type="password"
              id="password"
              className="w-full px-4 py-2 bg-white/10 border border-white/20 rounded-lg text-white placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-orange-400"
              placeholder="••••••••"
            />
          </div>
          <button
            type="submit"
            onClick={handleLogin}
            className="w-full py-3 bg-gradient-to-r from-orange-500 to-yellow-400 text-black font-semibold rounded-lg shadow-md hover:shadow-lg transition-shadow"
          >
            Sign In
          </button>
        </form>
        <div className="mt-6 text-center">
          <p className="text-sm text-gray-400">
            Don't have an account?{" "}
            <button className="text-orange-400 hover:underline">Sign up</button>
          </p>
        </div>
      </div>
    </section>
  );

  const renderFooter = () => (
    <footer className="py-8 px-4 bg-black/30 border-t border-white/10">
      <div className="max-w-6xl mx-auto flex flex-col md:flex-row justify-between items-center">
        <div className="flex items-center space-x-2 mb-4 md:mb-0">
          <svg viewBox="0 0 50 50" width="24" height="24" className="text-orange-400">
            <circle cx="25" cy="25" r="20" fill="currentColor" />
            <path
              d="M25 5v10M25 35v10M10.6 10.6l7.07 7.07m5.66 5.66a15 15 0 1 0 0-21.22"
              stroke="white"
              strokeWidth="2"
              fill="none"
            />
          </svg>
          <span className="text-white font-bold">FANALTIC</span>
        </div>
        <div className="text-gray-400 text-sm">
          &copy; {new Date().getFullYear()} FANALTIC. All rights reserved.
        </div>
      </div>
    </footer>
  );

  return (
    <div className={`min-h-screen flex flex-col ${isDarkMode ? "bg-gradient-to-br from-black via-gray-900 to-purple-950" : "bg-gray-100"} text-white`}>
      {/* Header */}
      <header className="sticky top-0 z-50 backdrop-blur-md bg-black/60 border-b border-white/10 px-4 py-4">
        <div className="max-w-6xl mx-auto flex justify-between items-center">
          {renderLogo()}
          {renderNav()}
          <div className="flex items-center space-x-4">
            <button
              onClick={() => setIsDarkMode(!isDarkMode)}
              className="p-2 rounded-full hover:bg-white/10 transition-colors"
            >
              <svg
                className="w-5 h-5"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                {isDarkMode ? (
                  <path
                    strokeLinecap="round"
                    strokeLinejoin="round"
                    strokeWidth="2"
                    d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z"
                  ></path>
                ) : (
                  <path
                    strokeLinecap="round"
                    strokeLinejoin="round"
                    strokeWidth="2"
                    d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"
                  ></path>
                )}
              </svg>
            </button>
            {!isLoggedIn ? (
              <button
                onClick={() => setCurrentPage("login")}
                className="hidden md:block px-4 py-2 bg-white/10 rounded-full text-sm hover:bg-white/20 transition-colors"
              >
                Login
              </button>
            ) : (
              <button
                onClick={handleLogout}
                className="hidden md:block px-4 py-2 bg-white/10 rounded-full text-sm hover:bg-white/20 transition-colors"
              >
                Logout
              </button>
            )}
          </div>
        </div>
        {renderMobileNav()}
      </header>

      {/* Main Content */}
      <main className="flex-grow">
        {currentPage === "home" && (
          <>
            {renderHero()}
            {renderSearchBar()}
            {renderBrowseSection()}
          </>
        )}
        {currentPage === "browse" && (
          <>
            {renderSearchBar()}
            {renderBrowseSection()}
          </>
        )}
        {currentPage === "player" && activeVideo && renderVideoPlayer()}
        {currentPage === "login" && renderLogin()}
      </main>

      {/* Footer */}
      {renderFooter()}
    </div>
  );  
}
```
