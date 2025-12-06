<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>PulseNews — Responsive Blogging Template</title>
  <meta name="description" content="A clean, responsive news/blog website template (single-file)." />
  <!-- Tailwind CDN (for quick prototyping) -->
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    /* small custom styles */
    .line-clamp-3 { display: -webkit-box; -webkit-line-clamp: 3; -webkit-box-orient: vertical; overflow: hidden; }
  </style>
</head>
<body class="bg-gray-50 text-gray-800 font-sans">
  <header class="bg-white shadow-sm sticky top-0 z-50">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16">
        <a href="#" class="flex items-center gap-3">
          <div class="w-10 h-10 rounded-full bg-gradient-to-tr from-indigo-600 to-pink-500 flex items-center justify-center text-white font-bold">PN</div>
          <div>
            <div class="text-lg font-extrabold">PulseNews</div>
            <div class="text-xs text-gray-500 -mt-1">Daily news & editorials</div>
          </div>
        </a>

        <nav class="hidden md:flex items-center gap-4">
          <button id="categoryAll" class="px-3 py-1 rounded hover:bg-gray-100">All</button>
          <button id="categoryTech" class="px-3 py-1 rounded hover:bg-gray-100">Tech</button>
          <button id="categoryWorld" class="px-3 py-1 rounded hover:bg-gray-100">World</button>
          <button id="categoryBusiness" class="px-3 py-1 rounded hover:bg-gray-100">Biz</button>
          <button id="categorySports" class="px-3 py-1 rounded hover:bg-gray-100">Sports</button>
        </nav>

        <div class="flex items-center gap-3">
          <div class="hidden sm:block">
            <input id="searchInput" type="search" placeholder="Search articles..." class="px-3 py-2 border rounded-md w-64" />
          </div>
          <button id="addPostBtn" class="bg-indigo-600 text-white px-3 py-2 rounded-md hover:opacity-90">Add Post</button>
          <button id="menuBtn" class="md:hidden p-2 rounded-md hover:bg-gray-100">☰</button>
        </div>
      </div>
    </div>
  </header>

  <main class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
    <section class="grid grid-cols-1 lg:grid-cols-3 gap-8">
      <!-- Featured area -->
      <div class="lg:col-span-2">
        <div id="featured" class="rounded-lg overflow-hidden shadow bg-white">
          <!-- injected by JS -->
        </div>

        <div class="mt-6 grid grid-cols-1 sm:grid-cols-2 gap-6" id="postsGrid">
          <!-- posts injected by JS -->
        </div>

        <div class="mt-6 flex justify-center">
          <button id="loadMore" class="px-4 py-2 border rounded">Load more</button>
        </div>
      </div>

      <!-- Sidebar -->
      <aside class="space-y-6">
        <div class="bg-white p-4 rounded shadow">
          <h3 class="font-bold">Subscribe</h3>
          <p class="text-sm text-gray-600">Get weekly highlights in your inbox.</p>
          <div class="mt-3 flex gap-2">
            <input id="emailInput" type="email" placeholder="you@email.com" class="px-3 py-2 border rounded w-full" />
            <button id="subscribeBtn" class="bg-indigo-600 text-white px-3 py-2 rounded">Go</button>
          </div>
        </div>

        <div class="bg-white p-4 rounded shadow">
          <h3 class="font-bold">Trending</h3>
          <ol id="trendingList" class="mt-3 text-sm text-gray-700 list-decimal list-inside space-y-2">
            <!-- trending items -->
          </ol>
        </div>

        <div class="bg-white p-4 rounded shadow">
          <h3 class="font-bold">About</h3>
          <p class="text-sm text-gray-600">PulseNews is a demo news/blogging template you can customize and deploy in minutes.</p>
        </div>
      </aside>
    </section>
  </main>

  <!-- Read modal -->
  <div id="modal" class="fixed inset-0 bg-black/40 hidden items-center justify-center z-50">
    <div class="bg-white rounded-lg max-w-3xl w-full mx-4 overflow-auto max-h-[90vh]">
      <div class="p-6">
        <button id="closeModal" class="float-right text-gray-500">✕</button>
        <h2 id="modalTitle" class="text-2xl font-bold"></h2>
        <p id="modalMeta" class="text-sm text-gray-500 mt-1"></p>
        <img id="modalImage" src="" alt="" class="mt-4 w-full rounded" />
        <div id="modalContent" class="mt-4 prose max-w-none"></div>
      </div>
    </div>
  </div>

  <!-- Simple Add Post panel -->
  <div id="editor" class="fixed right-6 bottom-6 bg-white shadow-lg rounded-lg p-4 w-96 hidden z-50">
    <h3 class="font-bold">Add / Edit Post</h3>
    <input id="postTitle" placeholder="Title" class="mt-2 w-full px-3 py-2 border rounded" />
    <input id="postAuthor" placeholder="Author" class="mt-2 w-full px-3 py-2 border rounded" />
    <select id="postCategory" class="mt-2 w-full px-3 py-2 border rounded">
      <option>Tech</option>
      <option>World</option>
      <option>Business</option>
      <option>Sports</option>
      <option>Opinion</option>
    </select>
    <input id="postImage" placeholder="Image URL (optional)" class="mt-2 w-full px-3 py-2 border rounded" />
    <textarea id="postExcerpt" placeholder="Short excerpt" class="mt-2 w-full px-3 py-2 border rounded" rows="3"></textarea>
    <textarea id="postBody" placeholder="Full content (HTML allowed)" class="mt-2 w-full px-3 py-2 border rounded" rows="6"></textarea>
    <div class="flex gap-2 mt-3">
      <button id="savePost" class="bg-indigo-600 text-white px-3 py-2 rounded">Save</button>
      <button id="cancelPost" class="px-3 py-2 border rounded">Cancel</button>
    </div>
  </div>

  <footer class="bg-white border-t mt-12">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-6 text-sm text-gray-600">
      © <span id="year"></span> PulseNews — Built with ❤️ • <span id="postCount">0</span> posts
    </div>
  </footer>

  <script>
    // ======== Simple in-browser data store (localStorage) ========
    const STORE_KEY = 'pulsenews_posts_v1';

    const samplePosts = [
      {
        id: 'p1', title: 'AI assistants change content creation', author: 'A. Verma', category: 'Tech', date: '2025-12-06',
        excerpt: 'How AI tools are reshaping short-form video and blogging workflows.',
        image: 'https://images.unsplash.com/photo-1555949963-aa79dcee9810?q=80&w=1400&auto=format&fit=crop&ixlib=rb-4.0.3&s=1',
        content: '<p>AI tools accelerate ideation and editing. Creators are experimenting with automated workflows...</p>'
      },
      {
        id: 'p2', title: 'Local teams win big in national tournament', author: 'S. Rao', category: 'Sports', date: '2025-12-04',
        excerpt: 'An exciting finals ended with a comeback in the last quarter.',
        image: 'https://images.unsplash.com/photo-1521412644187-c49fa049e84d?q=80&w=1400&auto=format&fit=crop',
        content: '<p>The game kept fans on edge. Highlights included...</p>'
      },
      {
        id: 'p3', title: 'Market roundup: Tech stocks bounce', author: 'R. Kapoor', category: 'Business', date: '2025-12-03',
        excerpt: 'Major indices recovered after two days of losses.',
        image: 'https://images.unsplash.com/photo-1542223616-0f5f5b3b6d6b?q=80&w=1400&auto=format&fit=crop',
        content: '<p>Markets saw a rotation into cyclical sectors...</p>'
      }
    ];

    function loadPosts() {
      const raw = localStorage.getItem(STORE_KEY);
      if (!raw) {
        localStorage.setItem(STORE_KEY, JSON.stringify(samplePosts));
        return samplePosts.slice();
      }
      try { return JSON.parse(raw); } catch(e) { localStorage.setItem(STORE_KEY, JSON.stringify(samplePosts)); return samplePosts.slice(); }
    }

    function savePosts(posts) { localStorage.setItem(STORE_KEY, JSON.stringify(posts)); }

    // ======== UI helpers ========
    const postsPerPage = 6;
    let allPosts = loadPosts().sort((a,b)=> new Date(b.date)-new Date(a.date));
    let currentPage = 1;
    let currentFilter = null;

    const featuredEl = document.getElementById('featured');
    const postsGrid = document.getElementById('postsGrid');
    const trendingList = document.getElementById('trendingList');
    const postCount = document.getElementById('postCount');
    document.getElementById('year').innerText = new Date().getFullYear();

    function renderFeatured() {
      const recent = allPosts[0];
      if (!recent) { featuredEl.innerHTML = '<div class="p-6">No posts yet</div>'; return; }
      featuredEl.innerHTML = `
        <img src="${recent.image || 'https://images.unsplash.com/photo-1503264116251-35a269479413?q=80&w=1400&auto=format&fit=crop'}" alt="" class="w-full h-64 object-cover">
        <div class="p-6">
          <div class="text-sm text-indigo-600 font-semibold">${recent.category}</div>
          <h2 class="text-2xl font-bold mt-2">${recent.title}</h2>
          <p class="mt-2 text-gray-600">${recent.excerpt}</p>
          <div class="mt-4 flex items-center gap-3 text-sm text-gray-500">
            <div>By ${recent.author}</div>
            <div>•</div>
            <div>${recent.date}</div>
            <button data-id="${recent.id}" class="ml-auto readBtn text-indigo-600 font-semibold">Read</button>
          </div>
        </div>
      `;
    }

    function renderPosts() {
      postsGrid.innerHTML = '';
      const filtered = allPosts.filter(p=> !currentFilter || p.category === currentFilter);
      const q = document.getElementById('searchInput').value.trim().toLowerCase();
      const searched = q ? filtered.filter(p=> (p.title+p.excerpt+p.content).toLowerCase().includes(q)) : filtered;
      const start = 0; // always show newest N; load more later
      const pageItems = searched.slice(0, currentPage*postsPerPage);

      pageItems.forEach(p=>{
        const card = document.createElement('article');
        card.className = 'bg-white rounded-lg shadow overflow-hidden';
        card.innerHTML = `
          <img src="${p.image || 'https://images.unsplash.com/photo-1503264116251-35a269479413?q=80&w=1200&auto=format&fit=crop'}" class="w-full h-40 object-cover">
          <div class="p-4">
            <div class="text-xs text-indigo-600 font-semibold">${p.category}</div>
            <h3 class="font-bold mt-1">${p.title}</h3>
            <p class="mt-2 text-sm text-gray-600 line-clamp-3">${p.excerpt}</p>
            <div class="mt-3 flex items-center text-sm text-gray-500">
              <div>${p.author}</div><div class="mx-2">•</div><div>${p.date}</div>
              <button data-id="${p.id}" class="ml-auto readBtn text-indigo-600 font-semibold">Read</button>
            </div>
          </div>
        `;
        postsGrid.appendChild(card);
      });

      postCount.innerText = allPosts.length;
      renderTrending();
      bindReadButtons();
    }

    function renderTrending(){
      const top = allPosts.slice(0,5);
      trendingList.innerHTML = '';
      top.forEach(p=>{
        const li = document.createElement('li');
        li.innerHTML = `<a href="#" class="hover:underline" data-id="${p.id}" onclick="openPostFromLink(event)">${p.title}</a>`;
        trendingList.appendChild(li);
      });
    }

    function bindReadButtons(){
      document.querySelectorAll('.readBtn').forEach(b=> b.addEventListener('click', (e)=>{
        const id = e.currentTarget.dataset.id; openModalFor(id);
      }));
    }

    function openModalFor(id){
      const p = allPosts.find(x=>x.id===id); if(!p) return;
      document.getElementById('modalTitle').innerText = p.title;
      document.getElementById('modalMeta').innerText = `${p.author} • ${p.date} • ${p.category}`;
      document.getElementById('modalImage').src = p.image || '';
      document.getElementById('modalContent').innerHTML = p.content || '<p>No content</p>';
      document.getElementById('modal').classList.remove('hidden');
    }

    function openPostFromLink(e){ e.preventDefault(); const id = e.currentTarget.dataset.id; openModalFor(id); }

    // ======== Events ========
    document.getElementById('closeModal').addEventListener('click', ()=> document.getElementById('modal').classList.add('hidden'));
    document.getElementById('menuBtn').addEventListener('click', ()=> alert('Mobile menu — customize as you like'));

    document.getElementById('addPostBtn').addEventListener('click', ()=> document.getElementById('editor').classList.toggle('hidden'));
    document.getElementById('cancelPost').addEventListener('click', ()=> { document.getElementById('editor').classList.add('hidden'); });

    document.getElementById('savePost').addEventListener('click', ()=>{
      const title = document.getElementById('postTitle').value.trim();
      const author = document.getElementById('postAuthor').value.trim() || 'Staff';
      const category = document.getElementById('postCategory').value;
      const image = document.getElementById('postImage').value.trim();
      const excerpt = document.getElementById('postExcerpt').value.trim();
      const body = document.getElementById('postBody').value.trim();
      if(!title || !excerpt || !body){ alert('Please add title, excerpt and body.'); return; }
      const newPost = { id: 'p'+Date.now(), title, author, category, image, excerpt, content: body, date: new Date().toISOString().slice(0,10) };
      allPosts.unshift(newPost); savePosts(allPosts); renderFeatured(); renderPosts(); document.getElementById('editor').classList.add('hidden');
      // clear fields
      ['postTitle','postAuthor','postImage','postExcerpt','postBody'].forEach(id=>document.getElementById(id).value='');
    });

    document.getElementById('searchInput').addEventListener('input', ()=> { currentPage=1; renderPosts(); });
    document.getElementById('loadMore').addEventListener('click', ()=>{ currentPage++; renderPosts(); });

    // category buttons
    document.getElementById('categoryAll').addEventListener('click', ()=>{ currentFilter=null; renderPosts(); });
    document.getElementById('categoryTech').addEventListener('click', ()=>{ currentFilter='Tech'; renderPosts(); });
    document.getElementById('categoryWorld').addEventListener('click', ()=>{ currentFilter='World'; renderPosts(); });
    document.getElementById('categoryBusiness').addEventListener('click', ()=>{ currentFilter='Business'; renderPosts(); });
    document.getElementById('categorySports').addEventListener('click', ()=>{ currentFilter='Sports'; renderPosts(); });

    // subscribe (demo)
    document.getElementById('subscribeBtn').addEventListener('click', ()=>{
      const em = document.getElementById('emailInput').value.trim();
      if(!em.includes('@')) { alert('Enter a valid email'); return; }
      alert('Thanks! (This is a demo — integrate an email provider to capture subscribers)');
      document.getElementById('emailInput').value='';
    });

    // quick init
    renderFeatured(); renderPosts();

    // expose a function so sidebar trending links work (inlined onclick uses global scope)
    window.openPostFromLink = openPostFromLink;

    // small UX: close modal on outside click
    document.getElementById('modal').addEventListener('click', (e)=>{ if(e.target.id==='modal') document.getElementById('modal').classList.add('hidden'); });

  </script>
</body>
</html>
