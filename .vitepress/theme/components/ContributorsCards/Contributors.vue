<script setup lang="ts">
import { computed, onMounted, ref, onUnmounted } from "vue";
import { useData } from "vitepress";
import VPTeamMembers from "vitepress/dist/client/theme-default/components/VPTeamMembers.vue";
import ContributorsItem from "./ContributorsItem.vue";
import { contributorsTranslations, type Lang } from "../../../data/i18n";
import { svgIcon } from "../../icon";

const { lang } = useData();
const t = computed(
	() =>
		contributorsTranslations[lang.value as Lang] ||
		contributorsTranslations["zh-CN"],
);

// 作者列表
const authors = computed(() => [
	{
		avatar: "https://github.com/LanRhyme.png?size=80",
		name: "LanRhyme",
		title: t.value.author,
		links: [
			{ icon: "github", link: "https://github.com/LanRhyme" },
			{
				icon: { svg: svgIcon.bilibili },
				link: "https://space.bilibili.com/496901387",
			},
		],
	},
	{
		avatar: "https://github.com/ChinsaaWei.png?size=80",
		name: "ChinsaaWei",
		title: t.value.author,
		links: [
			{ icon: "github", link: "https://github.com/ChinsaaWei" },
			{
				icon: { svg: svgIcon.bilibili },
				link: "https://space.bilibili.com/38902304",
			},
		],
	},
]);

// 贡献者数据类型
interface Contributor {
	avatar: string;
	name: string;
	title: string;
	link: string;
}

const contributors = ref<Contributor[]>([]);
const loading = ref(true);
const isVisible = ref(false);
const sectionRef = ref<HTMLElement | null>(null);

// 缓存配置
const CACHE_KEY = "contributors-cache";
const CACHE_TTL = 24 * 60 * 60 * 1000; // 24 小时

// 需要过滤的用户名
const excludeUsers = new Set([
	"LanRhyme",
	"ChinsaaWei",
	"dependabot[bot]",
	"crowdin-bot",
]);

// 缓存操作
function getCache(): { data: Contributor[]; lang: string } | null {
	try {
		const cached = localStorage.getItem(CACHE_KEY);
		if (!cached) return null;
		const { data, timestamp, lang } = JSON.parse(cached);
		if (Date.now() - timestamp > CACHE_TTL) {
			localStorage.removeItem(CACHE_KEY);
			return null;
		}
		return { data, lang };
	} catch {
		return null;
	}
}

function setCache(data: Contributor[]) {
	try {
		localStorage.setItem(
			CACHE_KEY,
			JSON.stringify({ data, timestamp: Date.now(), lang: lang.value }),
		);
	} catch {
		/* ignore */
	}
}

// 获取贡献者数据
async function fetchContributors() {
	const cached = getCache();
	if (cached?.lang === lang.value) {
		contributors.value = cached.data;
		loading.value = false;
		return;
	}

	try {
		const res = await fetch(
			"https://api.github.com/repos/LanRhyme/MicYou/stats/contributors",
		);
		const data = await res.json();

		if (!Array.isArray(data)) throw new Error("Data not ready");

		contributors.value = data
			.filter((c: { author?: { login: string } }) => {
				const login = c.author?.login;
				return login && !excludeUsers.has(login) && !login.includes("[bot]");
			})
			.sort((a: { total: number }, b: { total: number }) => b.total - a.total)
			.map(
				(c: {
					total: number;
					author: { login: string; avatar_url: string; html_url: string };
				}) => ({
					avatar: `${c.author.avatar_url}&size=80`,
					name: c.author.login,
					title: `${c.total} ${t.value.contributions}`,
					link: c.author.html_url,
				}),
			);

		setCache(contributors.value);
	} catch (err) {
		console.error("Failed to load contributors:", err);
		if (cached) contributors.value = cached.data;
	} finally {
		loading.value = false;
	}
}

// Intersection Observer 延迟加载
let observer: IntersectionObserver | null = null;

onMounted(() => {
	observer = new IntersectionObserver(
		([entry]) => {
			if (entry.isIntersecting && !isVisible.value) {
				isVisible.value = true;
				fetchContributors();
			}
		},
		{ rootMargin: "200px" },
	);
	if (sectionRef.value) observer.observe(sectionRef.value);
});

onUnmounted(() => observer?.disconnect());
</script>

<template>
  <section ref="sectionRef" class="contributors-section" aria-labelledby="contributors-title">
    <!-- 作者展示 - 使用 VitePress TeamMembers 组件 -->
    <div class="authors-wrapper">
      <h2 id="authors-title" class="section-title">
        {{ t.developedWith }}
      </h2>
      <VPTeamMembers size="small" :members="authors" />
    </div>

    <!-- 贡献者展示 - 使用 feature 风格卡片 -->
    <div v-if="contributors.length > 0" class="contributors-wrapper">
      <h2 id="contributors-title" class="section-title">
        {{ t.thanksContributors }}
      </h2>
      <ul class="contributors-grid" role="list">
        <li v-for="contributor in contributors" :key="contributor.name">
          <ContributorsItem :member="contributor" />
        </li>
      </ul>
    </div>
  </section>
</template>

<style scoped>
.contributors-section {
  margin-top: 48px;
  padding: 0 24px;
}

.authors-wrapper,
.contributors-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.section-title {
  text-align: center;
  color: var(--vp-c-text-2);
  font-size: 1.25rem;
  font-weight: 500;
  margin: 48px 0 24px;
  padding-bottom: 8px;
}

/* 作者卡片并排等宽撑满 */
.authors-wrapper {
  width: 100%;
}

.authors-wrapper :deep(.VPTeamMembers) {
  width: 100%;
}

.authors-wrapper :deep(.VPTeamMembers.small .container) {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 24px;
  width: 100%;
}

.authors-wrapper :deep(.VPTeamMembers.small .item) {
  width: 100%;
}

.contributors-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 24px;
  width: 100%;
  max-width: 1152px;
  margin: 0 auto;
  padding: 0;
  list-style: none;
}

/* 平板竖屏优化 */
@media (max-width: 768px) {
  .contributors-section {
    padding: 0 16px;
  }

  .section-title {
    margin: 32px 0 20px;
    font-size: 1.125rem;
  }

  .contributors-grid {
    gap: 16px;
  }
}

/* 手机竖屏优化 */
@media (max-width: 480px) {
  .contributors-section {
    margin-top: 32px;
    padding: 0 12px;
  }

  .section-title {
    margin: 24px 0 16px;
    font-size: 1rem;
    padding-bottom: 4px;
  }

  /* 作者卡片改为单列 */
  .authors-wrapper :deep(.VPTeamMembers.small .container) {
    grid-template-columns: 1fr;
    gap: 12px;
  }

  .contributors-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 12px;
  }
}
</style>