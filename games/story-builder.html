import React, { useState, useEffect } from 'react';
import { Tv, Users, Share2, Home, Plus, ThumbsUp, Clock, Book, Sparkles } from 'lucide-react';

const StoryBuilder = () => {
  const [mode, setMode] = useState('menu');
  const [displayMode, setDisplayMode] = useState(false);
  const [roomCode, setRoomCode] = useState('');
  const [playerName, setPlayerName] = useState('');
  const [genre, setGenre] = useState('fantasy');
  const [story, setStory] = useState([]);
  const [currentPrompts, setCurrentPrompts] = useState([]);
  const [myPrompt, setMyPrompt] = useState('');
  const [hasSubmitted, setHasSubmitted] = useState(false);
  const [votingPhase, setVotingPhase] = useState(false);
  const [myVote, setMyVote] = useState(null);
  const [timer, setTimer] = useState(60);
  const [players, setPlayers] = useState([]);
  const [showQR, setShowQR] = useState(false);
  const [isHost, setIsHost] = useState(false);

  const genres = [
    { id: 'fantasy', name: '⚔️ Fantasy', starter: 'In a realm where magic flows like rivers...' },
    { id: 'scifi', name: '🚀 Sci-Fi', starter: 'The year is 2247, and humanity has just discovered...' },
    { id: 'mystery', name: '🔍 Mystery', starter: 'The detective arrived at the mansion as thunder rumbled overhead...' },
    { id: 'romance', name: '💕 Romance', starter: 'Their eyes met across the crowded café, and time seemed to stop...' },
    { id: 'horror', name: '👻 Horror', starter: 'The old house on the hill had been abandoned for decades, until tonight...' },
    { id: 'comedy', name: '😂 Comedy', starter: 'It was a perfectly normal day, until the chicken learned to fly...' }
  ];

  useEffect(() => {
    const loadData = async () => {
      if (roomCode) {
        try {
          const storyData = await window.storage.get(`story:${roomCode}`, true);
          const promptsData = await window.storage.get(`prompts:${roomCode}`, true);
          const playersData = await window.storage.get(`players:${roomCode}`, true);
          const phaseData = await window.storage.get(`phase:${roomCode}`, true);
          
          if (storyData) setStory(JSON.parse(storyData.value));
          if (promptsData) setCurrentPrompts(JSON.parse(promptsData.value));
          if (playersData) setPlayers(JSON.parse(playersData.value));
          if (phaseData) {
            const phase = JSON.parse(phaseData.value);
            setVotingPhase(phase.state === 'voting');
          }
        } catch (e) {
          console.log('Loading room data');
        }
      }
    };
    
    if ((mode === 'game' || displayMode) && roomCode) {
      loadData();
      const interval = setInterval(loadData, 2000);
      return () => clearInterval(interval);
    }
  }, [mode, roomCode, displayMode]);

  useEffect(() => {
    if (votingPhase && timer > 0) {
      const interval = setInterval(() => setTimer(t => Math.max(0, t - 1)), 1000);
      return () => clearInterval(interval);
    }
    if (timer === 0 && votingPhase && mode === 'game') {
      endVoting();
    }
  }, [votingPhase, timer, mode]);

  const generateRoomCode = () => {
    return Math.random().toString(36).substring(2, 8).toUpperCase();
  };

  const createRoom = async () => {
    const code = generateRoomCode();
    setRoomCode(code);
    setIsHost(true);
    const selectedGenre = genres.find(g => g.id === genre);
    const initialStory = [{ text: selectedGenre.starter, author: 'Story', votes: 0 }];
    
    await window.storage.set(`story:${code}`, JSON.stringify(initialStory), true);
    await window.storage.set(`players:${code}`, JSON.stringify([{ name: playerName, id: Date.now() }]), true);
    await window.storage.set(`phase:${code}`, JSON.stringify({ state: 'writing', round: 1 }), true);
    await window.storage.set(`genre:${code}`, genre, true);
    
    setStory(initialStory);
    setPlayers([{ name: playerName, id: Date.now() }]);
    setMode('game');
  };

  const joinRoom = async () => {
    try {
      const storyData = await window.storage.get(`story:${roomCode}`, true);
      if (storyData) {
        const playersData = await window.storage.get(`players:${roomCode}`, true);
        const currentPlayers = playersData ? JSON.parse(playersData.value) : [];
        const newPlayer = { name: playerName, id: Date.now() };
        currentPlayers.push(newPlayer);
        
        setIsHost(false);
        await window.storage.set(`players:${roomCode}`, JSON.stringify(currentPlayers), true);
        setPlayers(currentPlayers);
        setMode('game');
      }
    } catch (e) {
      alert('Room not found!');
    }
  };

  const submitPrompt = async () => {
    if (myPrompt.trim() && !hasSubmitted) {
      try {
        const promptsData = await window.storage.get(`prompts:${roomCode}`, true);
        const currentPrompts = promptsData ? JSON.parse(promptsData.value) : [];
        currentPrompts.push({ text: myPrompt, author: playerName, votes: 0, id: Date.now() });
        
        await window.storage.set(`prompts:${roomCode}`, JSON.stringify(currentPrompts), true);
        setCurrentPrompts(currentPrompts);
        setHasSubmitted(true);
        setMyPrompt('');
        
        if (currentPrompts.length >= Math.max(2, players.length)) {
          await window.storage.set(`phase:${roomCode}`, JSON.stringify({ state: 'voting', round: story.length }), true);
          setVotingPhase(true);
          setTimer(60);
        }
      } catch (e) {
        console.error('Error submitting prompt:', e);
      }
    }
  };

  const vote = async (promptId) => {
    if (!myVote) {
      setMyVote(promptId);
      try {
        const promptsData = await window.storage.get(`prompts:${roomCode}`, true);
        const prompts = JSON.parse(promptsData.value);
        const prompt = prompts.find(p => p.id === promptId);
        if (prompt) {
          prompt.votes = (prompt.votes || 0) + 1;
          await window.storage.set(`prompts:${roomCode}`, JSON.stringify(prompts), true);
          setCurrentPrompts(prompts);
        }
      } catch (e) {
        console.error('Error voting:', e);
      }
    }
  };

  const endVoting = async () => {
    const winner = [...currentPrompts].sort((a, b) => (b.votes || 0) - (a.votes || 0))[0];
    if (winner) {
      try {
        const storyData = await window.storage.get(`story:${roomCode}`, true);
        const currentStory = JSON.parse(storyData.value);
        currentStory.push(winner);
        
        await window.storage.set(`story:${roomCode}`, JSON.stringify(currentStory), true);
        await window.storage.set(`prompts:${roomCode}`, JSON.stringify([]), true);
        await window.storage.set(`phase:${roomCode}`, JSON.stringify({ state: 'writing', round: currentStory.length }), true);
        
        setStory(currentStory);
        setCurrentPrompts([]);
        setVotingPhase(false);
        setHasSubmitted(false);
        setMyVote(null);
        setTimer(60);
      } catch (e) {
        console.error('Error ending voting:', e);
      }
    }
  };

  const saveStory = () => {
    const text = story.map(s => s.text).join(' ');
    const blob = new Blob([text], { type: 'text/plain' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `story-${roomCode}.txt`;
    a.click();
  };

  const getQRCode = () => {
    const url = window.location.href.split('?')[0] + '?room=' + roomCode;
    return `https://api.qrserver.com/v1/create-qr-code/?size=300x300&data=${encodeURIComponent(url)}`;
  };

  if (displayMode) {
    if (!roomCode) {
      return (
        <div className="min-h-screen bg-gradient-to-br from-slate-900 to-slate-800 text-white p-10 flex items-center justify-center">
          <div className="max-w-2xl w-full text-center">
            <h1 className="text-6xl font-bold mb-6">📺 TV Display Mode</h1>
            <p className="text-2xl opacity-80 mb-12">Enter a room code to spectate</p>
            <div className="bg-white bg-opacity-10 rounded-3xl p-12">
              <input
                type="text"
                placeholder="ROOM CODE"
                value={roomCode}
                onChange={(e) => setRoomCode(e.target.value.toUpperCase())}
                className="w-full p-6 rounded-xl text-3xl text-center uppercase font-bold mb-6 text-gray-900"
              />
              <button
                onClick={() => roomCode && setMode('game')}
                disabled={!roomCode}
                className="w-full p-6 rounded-xl bg-teal-500 text-white text-2xl font-bold mb-6 disabled:opacity-50 disabled:cursor-not-allowed hover:bg-teal-600 transition"
              >
                Connect to Room
              </button>
              <button
                onClick={() => setDisplayMode(false)}
                className="w-full p-6 rounded-xl border-2 border-white border-opacity-30 bg-transparent text-white text-2xl font-bold hover:bg-white hover:bg-opacity-10 transition"
              >
                Back to Menu
              </button>
            </div>
          </div>
        </div>
      );
    }

    return (
      <div className="min-h-screen bg-gradient-to-br from-slate-900 to-slate-800 text-white p-10">
        <div className="max-w-7xl mx-auto">
          <div className="flex justify-between items-center mb-10">
            <h1 className="text-5xl font-bold">📖 Story Builder</h1>
            <button onClick={() => { setDisplayMode(false); setRoomCode(''); }} className="bg-white bg-opacity-10 px-8 py-4 rounded-xl text-xl hover:bg-opacity-20 transition">
              Exit TV Mode
            </button>
          </div>

          <div className="bg-white bg-opacity-5 rounded-3xl p-10 mb-8">
            <div className="flex justify-between mb-8">
              <div>
                <div className="text-xl opacity-70">Room Code</div>
                <div className="text-5xl font-bold text-teal-400">{roomCode}</div>
              </div>
              <div>
                <div className="text-xl opacity-70">Players</div>
                <div className="text-5xl font-bold">{players.length} <Users className="inline" size={48} /></div>
              </div>
              <div>
                <div className="text-xl opacity-70">Phase</div>
                <div className={`text-5xl font-bold ${votingPhase ? 'text-red-400' : 'text-teal-400'}`}>
                  {votingPhase ? 'VOTING' : 'WRITING'}
                </div>
              </div>
            </div>
          </div>

          <div className="bg-white bg-opacity-5 rounded-3xl p-10 mb-8">
            <h2 className="text-4xl mb-8 flex items-center gap-4">
              <Book size={40} /> The Story So Far
            </h2>
            <div className="text-2xl leading-relaxed opacity-90">
              {story.map((s, i) => (
                <span key={i}>
                  {s.text}{i < story.length - 1 && ' '}
                </span>
              ))}
            </div>
          </div>

          {votingPhase && currentPrompts.length > 0 && (
            <div className="bg-white bg-opacity-5 rounded-3xl p-10">
              <div className="flex justify-between items-center mb-8">
                <h2 className="text-4xl flex items-center gap-4">
                  <ThumbsUp size={40} /> Vote for Next Sentence
                </h2>
                <div className="text-4xl text-red-400 font-bold">
                  <Clock className="inline" size={40} /> {timer}s
                </div>
              </div>
              <div className="space-y-6">
                {currentPrompts.map((p, i) => (
                  <div key={i} className="bg-white bg-opacity-10 rounded-2xl p-8 flex justify-between items-center">
                    <div>
                      <div className="text-2xl mb-3">{p.text}</div>
                      <div className="text-lg opacity-60">by {p.author}</div>
                    </div>
                    <div className="text-5xl font-bold text-teal-400">{p.votes || 0} votes</div>
                  </div>
                ))}
              </div>
            </div>
          )}
        </div>
      </div>
    );
  }

  if (mode === 'menu') {
    return (
      <div className="min-h-screen bg-gradient-to-br from-indigo-600 to-purple-700 flex items-center justify-center p-5">
        <div className="max-w-2xl w-full">
          <div className="text-center mb-10">
            <button onClick={() => window.location.href = '/'} className="bg-white bg-opacity-20 px-6 py-3 rounded-xl text-white mb-6 hover:bg-opacity-30 transition">
              <Home className="inline" size={20} /> Back to Games
            </button>
            <h1 className="text-6xl text-white font-bold mb-3">📖 Story Builder</h1>
            <p className="text-white text-opacity-90 text-xl">Create stories together, one sentence at a time</p>
          </div>

          <div className="bg-white rounded-3xl p-10 shadow-2xl">
            <input
              type="text"
              placeholder="Your name"
              value={playerName}
              onChange={(e) => setPlayerName(e.target.value)}
              className="w-full p-4 rounded-xl border-2 border-gray-300 text-lg mb-6"
            />

            <div className="mb-8">
              <label className="block mb-3 font-semibold text-gray-700">Choose Genre</label>
              <div className="grid grid-cols-2 gap-3">
                {genres.map(g => (
                  <button
                    key={g.id}
                    onClick={() => setGenre(g.id)}
                    className={`p-4 rounded-xl border-2 font-semibold text-lg transition ${
                      genre === g.id 
                        ? 'border-indigo-600 bg-indigo-50' 
                        : 'border-gray-300 bg-white hover:border-indigo-400'
                    }`}
                  >
                    {g.name}
                  </button>
                ))}
              </div>
            </div>

            <button
              onClick={createRoom}
              disabled={!playerName}
              className="w-full p-5 rounded-xl bg-gradient-to-r from-indigo-600 to-purple-700 text-white text-xl font-bold mb-4 disabled:opacity-50 disabled:cursor-not-allowed hover:shadow-lg transition"
            >
              <Plus className="inline mr-2" size={24} />
              Create New Story
            </button>

            <div className="text-center my-6 text-gray-400">or</div>

            <input
              type="text"
              placeholder="Room code"
              value={roomCode}
              onChange={(e) => setRoomCode(e.target.value.toUpperCase())}
              className="w-full p-4 rounded-xl border-2 border-gray-300 text-lg mb-4 uppercase"
            />

            <button
              onClick={joinRoom}
              disabled={!playerName || !roomCode}
              className="w-full p-5 rounded-xl bg-teal-500 text-white text-xl font-bold mb-6 disabled:opacity-50 disabled:cursor-not-allowed hover:bg-teal-600 transition"
            >
              Join Story
            </button>

            <div className="text-center my-6 text-gray-400">or</div>

            <button
              onClick={() => setDisplayMode(true)}
              className="w-full p-5 rounded-xl border-2 border-purple-700 text-purple-700 text-xl font-bold hover:bg-purple-50 transition"
            >
              <Tv className="inline mr-2" size={24} />
              Launch TV Display Mode
            </button>
          </div>
        </div>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-gradient-to-br from-indigo-600 to-purple-700 p-5">
      <div className="max-w-4xl mx-auto">
        <div className="flex justify-between items-center mb-6">
          <button onClick={() => setMode('menu')} className="bg-white bg-opacity-20 px-6 py-3 rounded-xl text-white hover:bg-opacity-30 transition">
            <Home className="inline" size={20} /> Exit
          </button>
          <div className="flex gap-3">
            <button onClick={() => setShowQR(!showQR)} className="bg-white bg-opacity-20 px-6 py-3 rounded-xl text-white hover:bg-opacity-30 transition">
              <Share2 className="inline" size={20} /> QR
            </button>
            <button onClick={() => setDisplayMode(true)} className="bg-white bg-opacity-20 px-6 py-3 rounded-xl text-white hover:bg-opacity-30 transition">
              <Tv className="inline" size={20} /> TV Mode
            </button>
            <button onClick={saveStory} className="bg-white bg-opacity-20 px-6 py-3 rounded-xl text-white hover:bg-opacity-30 transition">
              Save Story
            </button>
          </div>
        </div>

        {showQR && (
          <div className="bg-white rounded-3xl p-8 mb-6 text-center">
            <h3 className="text-2xl font-bold mb-6">Scan to Join</h3>
            <img src={getQRCode()} alt="QR Code" className="mx-auto max-w-xs" />
            <div className="mt-6 text-3xl font-bold text-indigo-600">{roomCode}</div>
          </div>
        )}

        <div className="bg-white rounded-3xl p-8 mb-6">
          <div className="flex justify-between mb-6">
            <div>
              <div className="text-sm text-gray-500">Room Code</div>
              <div className="text-3xl font-bold text-indigo-600">{roomCode}</div>
            </div>
            <div>
              <div className="text-sm text-gray-500">Players</div>
              <div className="text-3xl font-bold"><Users className="inline" size={32} /> {players.length}</div>
            </div>
          </div>
          <div className="text-sm text-gray-500">Players: {players.map(p => p.name).join(', ')}</div>
        </div>

        <div className="bg-white rounded-3xl p-8 mb-6">
          <h2 className="text-2xl font-bold mb-6 flex items-center gap-3">
            <Book size={28} /> The Story
          </h2>
          <div className="text-lg leading-relaxed text-gray-700">
            {story.map((s, i) => (
              <span key={i}>
                {s.text}{i < story.length - 1 && ' '}
              </span>
            ))}
          </div>
        </div>

        {!votingPhase && !hasSubmitted && (
          <div className="bg-white rounded-3xl p-8">
            <h3 className="text-xl font-bold mb-4">Add Your Sentence</h3>
            <textarea
              value={myPrompt}
              onChange={(e) => setMyPrompt(e.target.value)}
              placeholder="Write the next sentence..."
              className="w-full p-4 rounded-xl border-2 border-gray-300 text-lg mb-4 resize-y min-h-32"
            />
            <button
              onClick={submitPrompt}
              disabled={!myPrompt.trim()}
              className="w-full p-4 rounded-xl bg-gradient-to-r from-indigo-600 to-purple-700 text-white text-lg font-bold disabled:opacity-50 disabled:cursor-not-allowed hover:shadow-lg transition"
            >
              Submit Sentence
            </button>
          </div>
        )}

        {!votingPhase && hasSubmitted && (
          <div className="bg-white rounded-3xl p-8 text-center">
            <Sparkles className="mx-auto text-teal-500 mb-4" size={48} />
            <h3 className="text-2xl font-bold">Sentence Submitted!</h3>
            <p className="text-gray-600 mt-3">Waiting for other players...</p>
          </div>
        )}

        {votingPhase && (
          <div className="bg-white rounded-3xl p-8">
            <div className="flex justify-between items-center mb-6">
              <h3 className="text-xl font-bold">Vote for Next Sentence</h3>
              <div className="text-2xl font-bold text-red-500">
                <Clock className="inline" size={24} /> {timer}s
              </div>
            </div>
            <div className="space-y-4">
              {currentPrompts.map((p, i) => (
                <div
                  key={i}
                  onClick={() => vote(p.id)}
                  className={`p-6 rounded-xl border-2 transition cursor-pointer ${
                    myVote === p.id 
                      ? 'border-teal-500 bg-teal-50' 
                      : 'border-gray-300 hover:border-teal-300'
                  } ${myVote && 'cursor-default'}`}
                >
                  <div className="text-lg mb-3">{p.text}</div>
                  <div className="flex justify-between text-sm text-gray-600">
                    <span>by {p.author}</span>
                    <span><ThumbsUp className="inline" size={16} /> {p.votes || 0} votes</span>
                  </div>
                </div>
              ))}
            </div>
          </div>
        )}
      </div>
    </div>
  );
};

export default StoryBuilder;
