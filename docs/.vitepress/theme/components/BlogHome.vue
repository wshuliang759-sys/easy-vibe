<script setup>
import { computed, ref } from 'vue'

const activeTopic = ref('全部')
const email = ref('')
const subscribed = ref(false)

const topics = ['全部', 'AI 与创作', '产品思考', '生活随笔']
const posts = [
  { topic: 'AI 与创作', date: '2026.09.08', read: '6 分钟', title: '别急着让 AI 写完一切', excerpt: '真正重要的不是更快地产出答案，而是学会把问题问得更深、更具体。', accent: 'violet', number: '01' },
  { topic: '产品思考', date: '2026.08.24', read: '8 分钟', title: '一个好产品，先照顾人的犹豫', excerpt: '设计不是替用户做决定，而是让每一次选择都感到笃定与轻松。', accent: 'orange', number: '02' },
  { topic: '生活随笔', date: '2026.08.11', read: '4 分钟', title: '在普通日子里，收集微小的确定性', excerpt: '一杯热咖啡、准时的日落，还有那些不必解释的安静时刻。', accent: 'blue', number: '03' },
  { topic: 'AI 与创作', date: '2026.07.29', read: '7 分钟', title: '把灵感变成作品的最短路径', excerpt: '先做一个粗糙但完整的版本，再让它在反馈中慢慢长出枝叶。', accent: 'green', number: '04' }
]

const visiblePosts = computed(() => activeTopic.value === '全部'
  ? posts
  : posts.filter((post) => post.topic === activeTopic.value))

const subscribe = () => {
  if (email.value.trim()) subscribed.value = true
}
</script>

<template>
  <main class="journal">
    <nav class="journal-nav" aria-label="主导航">
      <a class="journal-logo" href="#top" aria-label="回到首页">north<span>.</span></a>
      <div class="journal-nav-links">
        <a href="#articles">文章</a><a href="#about">关于</a>
      </div>
      <a class="nav-note" href="#newsletter">订阅周报 <span>↗</span></a>
    </nav>

    <section id="top" class="journal-hero">
      <p class="eyebrow">PERSONAL JOURNAL · 2026</p>
      <h1>慢一点，<br><em>也没关系。</em></h1>
      <div class="hero-bottom">
        <p>记录关于创作、产品与生活的思考。<br>愿每一段文字，都能为你留下一点光。</p>
        <a href="#articles" class="circle-link" aria-label="浏览文章">↓</a>
      </div>
      <div class="sun-orbit" aria-hidden="true"><i></i><b></b></div>
    </section>

    <section id="articles" class="article-section">
      <div class="section-title"><p>SELECTED NOTES</p><h2>最近写的</h2></div>
      <div class="topic-row" aria-label="文章分类">
        <button v-for="topic in topics" :key="topic" :class="{ active: activeTopic === topic }" @click="activeTopic = topic">{{ topic }}</button>
      </div>
      <div class="post-list">
        <article v-for="post in visiblePosts" :key="post.number" class="post-card">
          <div class="post-art" :class="post.accent"><span>{{ post.number }}</span><div class="art-shape"></div></div>
          <div class="post-copy"><div class="post-meta"><span>{{ post.topic }}</span><span>{{ post.date }} · {{ post.read }}</span></div><h3>{{ post.title }}</h3><p>{{ post.excerpt }}</p><a href="#newsletter">阅读全文 <span>→</span></a></div>
        </article>
      </div>
    </section>

    <section id="about" class="about-section">
      <div class="portrait" aria-hidden="true"><span>✦</span></div>
      <div><p class="eyebrow">HELLO, I AM LIN</p><h2>把好奇心，<br>写成一封封信。</h2><p class="about-text">我是 Lin，一名产品设计师与长期主义者。这里没有标准答案，只有正在发生的观察、实验和一点点真诚的分享。</p><a href="mailto:hello@example.com" class="text-link">认识我一下 <span>→</span></a></div>
    </section>

    <section id="newsletter" class="newsletter">
      <p class="eyebrow">A LETTER, OCCASIONALLY</p>
      <h2>收到一封<br><em>慢一点的信。</em></h2>
      <p>不定期分享新的文章、灵感碎片和有趣的发现。</p>
      <form @submit.prevent="subscribe">
        <label class="sr-only" for="email">邮箱地址</label>
        <input id="email" v-model="email" type="email" required placeholder="你的邮箱地址" :disabled="subscribed">
        <button type="submit" :disabled="subscribed">{{ subscribed ? '已订阅，谢谢！' : '订阅 →' }}</button>
      </form>
    </section>

    <footer><span>© 2026 NORTH JOURNAL</span><span>MADE WITH CALM & CARE</span></footer>
  </main>
</template>

<style scoped>
.journal{--ink:#19231f;--cream:#f5f1e8;--paper:#fcfaf5;--orange:#e7653c;--line:#d9d5ca;color:var(--ink);background:var(--paper);font-family:Georgia,'Noto Serif SC',serif;min-height:100vh}.journal-nav{height:78px;padding:0 clamp(24px,6vw,92px);display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid var(--line);font-family:Arial,sans-serif}.journal-logo{font:700 29px/1 Georgia,serif;letter-spacing:-2px;color:var(--ink);text-decoration:none}.journal-logo span{color:var(--orange)}.journal-nav-links{display:flex;gap:28px;margin-left:12%}.journal-nav a{color:var(--ink);text-decoration:none;font-size:14px}.nav-note{border-bottom:1px solid var(--ink);padding-bottom:3px}.nav-note span{color:var(--orange)}.journal-hero{position:relative;overflow:hidden;min-height:580px;padding:clamp(70px,10vw,140px) clamp(24px,12vw,180px) 60px;background:var(--cream)}.eyebrow{font:600 11px/1.3 Arial,sans-serif;letter-spacing:1.6px;margin:0 0 20px;color:#69746d}.journal-hero h1,.newsletter h2,.about-section h2{position:relative;z-index:1;margin:0;font-size:clamp(58px,8.5vw,128px);line-height:.93;font-weight:400;letter-spacing:-.07em}.journal h1 em,.newsletter em{font-weight:400;color:var(--orange)}.hero-bottom{position:relative;z-index:1;display:flex;align-items:end;justify-content:space-between;max-width:680px;margin-top:54px;font-size:16px;line-height:1.65}.circle-link{width:52px;height:52px;border:1px solid var(--ink);border-radius:50%;display:grid;place-items:center;color:var(--ink);text-decoration:none;font:27px Arial;transition:.2s}.circle-link:hover{background:var(--ink);color:#fff}.sun-orbit{position:absolute;right:10%;top:86px;width:310px;height:310px;border-radius:50%;border:1px solid #bdc6b2}.sun-orbit i{position:absolute;inset:48px;border-radius:50%;background:#dcce61}.sun-orbit b{position:absolute;width:13px;height:13px;border-radius:50%;background:var(--orange);bottom:38px;left:40px}.article-section{padding:110px clamp(24px,12vw,180px)}.section-title{display:flex;justify-content:space-between;align-items:end;border-bottom:1px solid var(--ink);padding-bottom:20px}.section-title p{font:600 11px Arial,sans-serif;letter-spacing:1.5px}.section-title h2{margin:0;font-size:42px;font-weight:400;letter-spacing:-.05em}.topic-row{display:flex;gap:10px;padding:28px 0}.topic-row button{border:1px solid var(--line);background:transparent;border-radius:20px;padding:8px 14px;color:var(--ink);cursor:pointer}.topic-row button.active,.topic-row button:hover{background:var(--ink);color:white;border-color:var(--ink)}.post-list{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:28px}.post-card{border-top:1px solid var(--line);padding-top:20px}.post-art{height:200px;position:relative;overflow:hidden;margin-bottom:23px}.post-art span{position:absolute;top:18px;left:19px;font:11px Arial;color:var(--ink);z-index:2}.post-art.violet{background:#c7bcdf}.post-art.orange{background:#ec9d75}.post-art.blue{background:#a8ced1}.post-art.green{background:#b8c89e}.art-shape{position:absolute;width:150px;height:150px;border-radius:50%;background:#f7f2df;right:13%;bottom:-43px}.orange .art-shape{width:120px;height:170px;border-radius:60px 60px 0 0;background:#563f36;right:22%}.blue .art-shape{width:260px;height:54px;border-radius:50%;background:#305b62;right:-8%;bottom:42px}.green .art-shape{border-radius:0;transform:rotate(35deg);bottom:-75px;right:23%;background:#e8e38a}.post-meta{display:flex;justify-content:space-between;font:11px Arial;color:#6e756f}.post-meta span:first-child{color:var(--orange);font-weight:bold}.post-copy h3{font-size:26px;letter-spacing:-.04em;font-weight:400;margin:14px 0 10px}.post-copy p,.about-text,.newsletter>p{font-size:15px;line-height:1.7;color:#58625d;margin:0 0 16px}.post-copy a,.text-link{color:var(--ink);font:13px Arial;text-decoration:none;border-bottom:1px solid var(--ink);padding-bottom:3px}.post-copy a span,.text-link span{color:var(--orange);padding-left:4px}.about-section{display:grid;grid-template-columns:1fr 1.3fr;gap:clamp(40px,10vw,150px);align-items:center;background:#dce2d2;padding:100px clamp(24px,12vw,180px)}.portrait{height:315px;background:#22352e;position:relative;overflow:hidden}.portrait:before{content:'';position:absolute;width:180px;height:210px;border-radius:90px 90px 28px 28px;background:#e0a076;left:50%;bottom:-22px;transform:translateX(-50%)}.portrait:after{content:'';position:absolute;width:120px;height:105px;background:#2c221d;border-radius:60px 60px 30px 30px;left:50%;top:62px;transform:translateX(-50%)}.portrait span{position:absolute;color:#f4df74;font-size:34px;right:20%;top:20%;z-index:1}.about-section h2{font-size:clamp(42px,5vw,72px);margin-bottom:23px}.about-text{max-width:410px}.newsletter{text-align:center;padding:118px 24px;background:var(--cream)}.newsletter h2{font-size:clamp(47px,6.5vw,92px);margin-bottom:25px}.newsletter form{display:flex;max-width:440px;margin:29px auto 0;border-bottom:1px solid var(--ink)}.newsletter input{flex:1;border:0;background:transparent;padding:13px 0;outline:0;font:15px Georgia}.newsletter button{border:0;background:transparent;cursor:pointer;color:var(--orange);font:600 13px Arial;padding:0 0 0 12px}.newsletter button:disabled{color:#6d756f}footer{display:flex;justify-content:space-between;padding:26px clamp(24px,6vw,92px);background:var(--ink);color:#eef1e8;font:10px Arial;letter-spacing:1.2px}.sr-only{position:absolute;width:1px;height:1px;padding:0;margin:-1px;overflow:hidden;clip:rect(0,0,0,0);white-space:nowrap;border:0}@media(max-width:700px){.journal-nav-links{display:none}.journal-hero{min-height:520px}.sun-orbit{width:220px;height:220px;right:-40px;top:235px}.sun-orbit i{inset:35px}.hero-bottom{margin-top:46px;gap:18px}.article-section{padding-top:72px;padding-bottom:72px}.post-list{grid-template-columns:1fr}.about-section{grid-template-columns:1fr;padding-top:70px;padding-bottom:70px}.portrait{height:220px}.newsletter{padding-top:80px;padding-bottom:80px}footer{font-size:8px;gap:12px}.section-title h2{font-size:34px}}
</style>
