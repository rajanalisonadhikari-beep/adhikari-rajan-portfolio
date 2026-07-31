// Loads content from /content/*.json and renders it. Falls back to built-in
// defaults so the page never looks empty. Edits made in /admin update the JSON.

async function getJSON(path, fallback){
  try{
    const res = await fetch(path, {cache:'no-store'});
    if(!res.ok) throw new Error(res.status);
    return await res.json();
  }catch(e){ console.warn('Using fallback for', path, e); return fallback; }
}

function mdToHtml(md){
  if(!md) return '';
  if(window.marked){ return window.marked.parse(md); }
  return md.split(/\n{2,}/).map(p=>'<p>'+p.replace(/\n/g,'<br>')+'</p>').join('');
}
function esc(s){return (s||'').replace(/[&<>"]/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c]));}

const ICONS={'Trekking & Expeditions':'⛰️','Barbershop':'✂️','Imports':'📦'};

async function render(){
  const site = await getJSON('content/site.json', window.__DEFAULTS.site);
  const ventures = await getJSON('content/ventures.json', window.__DEFAULTS.ventures);
  const blog = await getJSON('content/blog.json', window.__DEFAULTS.blog);

  // Brand + hero
  document.title = site.name + ' — Portfolio';
  document.querySelectorAll('[data-name]').forEach(el=>el.textContent=site.name);
  const initials = site.name.split(' ').map(w=>w[0]).join('').slice(0,2).toUpperCase();
  document.getElementById('brand-mark').textContent = initials;
  document.getElementById('hero-tagline').textContent = site.tagline;
  document.getElementById('hero-intro').textContent = site.heroIntro;

  // About
  document.getElementById('about-heading').textContent = site.aboutHeading || 'About Me';
  document.getElementById('about-body').innerHTML = mdToHtml(site.about);
  const photoWrap = document.getElementById('about-photo');
  if(site.photo){ photoWrap.outerHTML = '<img id="about-photo" class="about-photo" alt="'+esc(site.name)+'" src="'+esc(site.photo)+'">'; }

  // Ventures
  const cards = (ventures.items||[]).map(v=>{
    const thumb = v.image ? '<img src="'+esc(v.image)+'" alt="'+esc(v.name)+'">' : (ICONS[v.name]||'⭐');
    const link = v.link ? '<a class="more" href="'+esc(v.link)+'" target="_blank" rel="noopener">Learn more →</a>' : '';
    return '<article class="card"><div class="thumb">'+thumb+'</div><div class="body">'+
      '<span class="cat">'+esc(v.category)+'</span><h3>'+esc(v.name)+'</h3><p>'+esc(v.description)+'</p>'+link+'</div></article>';
  }).join('');
  document.getElementById('ventures-grid').innerHTML = cards;

  // Blog
  const posts = (blog.posts||[]).slice().sort((a,b)=> (b.date||'').localeCompare(a.date||''));
  const blogSection = document.getElementById('blog');
  if(posts.length){
    document.getElementById('posts-grid').innerHTML = posts.map(p=>{
      const d = p.date ? new Date(p.date).toLocaleDateString('en-US',{year:'numeric',month:'short',day:'numeric'}) : '';
      return '<article class="post"><div class="date">'+esc(d)+'</div><h3>'+esc(p.title)+'</h3><p>'+esc(p.summary)+'</p></article>';
    }).join('');
  }else if(blogSection){ blogSection.style.display='none'; }

  // Contact
  document.getElementById('contact-email').textContent = site.email;
  document.getElementById('contact-email').href = 'mailto:'+site.email;
  const loc = document.getElementById('contact-location');
  loc.textContent = [site.location, site.phone].filter(Boolean).join(' • ');
  document.getElementById('socials').innerHTML = (site.socials||[]).filter(s=>s.url&&s.url!=='#')
    .map(s=>'<a href="'+esc(s.url)+'" target="_blank" rel="noopener">'+esc(s.platform)+'</a>').join('');
  document.getElementById('year').textContent = new Date().getFullYear();
}

// mobile nav
document.addEventListener('click', e=>{
  if(e.target.closest('#nav-toggle')){ document.getElementById('nav-links').classList.toggle('open'); }
  else if(e.target.closest('#nav-links a')){ document.getElementById('nav-links').classList.remove('open'); }
});

render();
