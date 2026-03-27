# gentheme
universe inspired theme for imgui menues (works for VR and standlone imgui



```
struct Star
{
	ImVec2 pos;
	float speed;
	float size;
};

static std::vector<Star> stars;
static bool starsInit = false;

void InitStars(int count, ImVec2 size)
{
	stars.clear();

	for (int i = 0; i < count; i++)
	{
		Star s;

		s.pos = ImVec2(
			(float)(rand() % (int)size.x),
			(float)(rand() % (int)size.y)
		);

		s.speed = 0.3f + (rand() % 100) / 200.0f;
		s.size = 1.0f + (rand() % 3);

		stars.push_back(s);
	}

	starsInit = true;
}



void DrawStars(ImDrawList* draw, ImVec2 pos, ImVec2 size)
{
	if (!starsInit)
		InitStars(100, size);

	for (auto& s : stars)
	{
		s.pos.y += s.speed;

		if (s.pos.y > size.y)
		{
			s.pos.y = 0;
			s.pos.x = (float)(rand() % (int)size.x);
		}

		draw->AddCircleFilled(
			ImVec2(pos.x + s.pos.x, pos.y + s.pos.y),
			s.size,
			IM_COL32(200, 150, 255, 200)
		);
	}
}



void DrawBlur(ImDrawList* draw, ImVec2 pos, ImVec2 size)
{
	draw->AddRectFilled(
		pos,
		ImVec2(pos.x + size.x, pos.y + size.y),
		IM_COL32(20, 10, 40, 180),
		12.0f
	);
}



void SetGalaxyTheme()
{
	ImGuiStyle& style = ImGui::GetStyle();
	ImVec4* colors = style.Colors;

	colors[ImGuiCol_WindowBg] = ImVec4(0.05f, 0.02f, 0.08f, 1.00f);
	colors[ImGuiCol_Text] = ImVec4(0.95f, 0.90f, 1.00f, 1.00f);

	colors[ImGuiCol_Button] = ImVec4(0.35f, 0.15f, 0.55f, 0.80f);
	colors[ImGuiCol_ButtonHovered] = ImVec4(0.55f, 0.25f, 0.85f, 0.90f);
	colors[ImGuiCol_ButtonActive] = ImVec4(0.65f, 0.30f, 0.95f, 1.00f);

	style.WindowRounding = 12.0f;
	style.FrameRounding = 8.0f;
	style.TabRounding = 10.0f;
}



```
