/* See LICENSE file for copyright and license details. */

#define XF86AudioPrev           0x1008ff16
#define XF86AudioPlay           0x1008ff14
#define XF86AudioNext           0x1008ff17
#define XF86AudioMute           0x1008ff12
#define XF86AudioLowerVolume    0x1008ff11
#define XF86AudioRaiseVolume    0x1008ff13

/* appearance */
static const unsigned int borderpx  = 2;        /* border pixel of windows */
static const unsigned int gappx     = 32;        /* gaps between windows */
static const unsigned int snap      = 32;       /* snap pixel */
static const int showbar            = 1;        /* 0 means no bar */
static const int topbar             = 1;        /* 0 means bottom bar */
static const char *fonts[]          = { "JetBrains Mono:size=10", "Material Icons Outlined:pixelsize=22" };
static const char dmenufont[]       = "JetBrains Mono:size=10";
static const char col_gray1[]       = "#2e3440";
static const char col_gray2[]       = "#3b4252";
static const char col_gray3[]       = "#d8dee9";
static const char col_blue[]        = "#5e81ac";
static const char col_lblue[]       = "#81a1c1";
static const char col_cyan[]        = "#8fbcbb";
static const char col_indigo[]      = "#88c0d0";
static const char col_violet[]      = "#b48ead";
static const char *colors[][3]      = {
	/*               fg         bg         border   */
	[SchemeNorm] = { col_gray3, col_gray1, col_gray2 },
	[SchemeSel]  = { col_blue, col_gray1,  col_blue },
	[SchemeBorder] = { col_gray2, col_gray1, col_gray1 },
	[SchemeBackground] = { col_gray1, col_gray1, col_gray1 },
	[SchemeLblue] = { col_lblue, col_gray1, col_gray1 },
	[SchemeCyan] = { col_cyan, col_gray1, col_gray1 },
	[SchemeIndigo] = { col_indigo, col_gray1, col_gray1 },
	[SchemeViolet] = { col_violet, col_gray1, col_gray1 },
};

/* tagging */
static const char *tags[] = { "1", "2", "3", "4", "5", "6", "7", "8", "9" };

static const Rule rules[] = {
	/* xprop(1):
	 *	WM_CLASS(STRING) = instance, class
	 *	WM_NAME(STRING) = title
	 */
	/* class      instance    title       tags mask     isfloating   monitor */
	{ "discord",  NULL,       NULL,       0,            1,           -1 },
	{ "Steam",    NULL,       NULL,       0,            1,           -1 },
	{ "multimc",  NULL,       NULL,       0,            1,           -1 },
	{ "MultiMC5", NULL,       NULL,       0,            1,           -1 },
};

/* layout(s) */
static const float mfact     = 0.5;  /* factor of master area size [0.05..0.95] */
static const int nmaster     = 1;    /* number of clients in master area */
static const int resizehints = 1;    /* 1 means respect size hints in tiled resizals */

static const Layout layouts[] = {
	/* symbol     arrange function */
	{ "[T]",      tile },    /* first entry is default */
	{ "[F]",      NULL },    /* no layout function means floating behavior */
	{ "[M]",      monocle },
};

/* key definitions */
#define MODKEY Mod1Mask
#define TAGKEYS(KEY,TAG) \
	{ MODKEY,                       KEY,      view,           {.ui = 1 << TAG} }, \
	{ MODKEY|ControlMask,           KEY,      toggleview,     {.ui = 1 << TAG} }, \
	{ MODKEY|ShiftMask,             KEY,      tag,            {.ui = 1 << TAG} }, \
	{ MODKEY|ControlMask|ShiftMask, KEY,      toggletag,      {.ui = 1 << TAG} },

/* helper for spawning shell commands in the pre dwm-5.0 fashion */
#define SHCMD(cmd) { .v = (const char*[]){ "/bin/sh", "-c", cmd, NULL } }

/* commands */
static char dmenumon[2] = "0"; /* component of dmenucmd, manipulated in spawn() */
static const char *dmenucmd[] = { "dmenu_run", "-m", dmenumon, "-fn", dmenufont, "-nb", col_gray1, "-nf", col_gray3, "-sb", col_gray1, "-sf", col_blue, "-h", "32", NULL };
static const char *termcmd[]  = { "st", NULL };
static const char *slockcmd[]  = { "slock", NULL };
static const char *firefoxcmd[]  = { "firefox-bin", NULL };
static const char *powercmd[] = { "power.sh", "-m", dmenumon, "-fn", dmenufont, "-nb", col_gray1, "-nf", col_gray3, "-sb", col_gray1, "-sf", col_blue, "-h", "32", NULL };

static const char *prevcmd[] = { "playerctl", "previous", NULL };
static const char *nextcmd[] = { "playerctl", "next", NULL };
static const char *playcmd[] = { "playerctl", "play-pause", NULL };
static const char *mutecmd[] = { "amixer", "set", "Master", "toggle", NULL };
static const char *lowercmd[] = { "amixer", "set", "Master", "5%-", NULL };
static const char *raisecmd[] = { "amixer", "set", "Master", "5%+", NULL };

static Key keys[] = {
	/* modifier                     key        function        argument */
	{ MODKEY,                       XK_p,      spawn,          {.v = dmenucmd } },
	{ MODKEY|ShiftMask,             XK_Return, spawn,          {.v = termcmd } },
	{ MODKEY,                       XK_b,      togglebar,      {0} },
	{ MODKEY,                       XK_j,      focusstack,     {.i = +1 } },
	{ MODKEY,                       XK_k,      focusstack,     {.i = -1 } },
	{ MODKEY,                       XK_i,      incnmaster,     {.i = +1 } },
	{ MODKEY,                       XK_d,      incnmaster,     {.i = -1 } },
	{ MODKEY,                       XK_h,      setmfact,       {.f = -0.05} },
	{ MODKEY,                       XK_l,      setmfact,       {.f = +0.05} },
	{ MODKEY,                       XK_Return, zoom,           {0} },
	{ MODKEY,                       XK_Tab,    view,           {0} },
	{ MODKEY|ShiftMask,             XK_c,      killclient,     {0} },
	{ MODKEY,                       XK_t,      setlayout,      {.v = &layouts[0]} },
	{ MODKEY,                       XK_f,      setlayout,      {.v = &layouts[1]} },
	{ MODKEY,                       XK_m,      setlayout,      {.v = &layouts[2]} },
	{ MODKEY,                       XK_space,  setlayout,      {0} },
	{ MODKEY|ShiftMask,             XK_space,  togglefloating, {0} },
	{ MODKEY,                       XK_0,      view,           {.ui = ~0 } },
	{ MODKEY|ShiftMask,             XK_0,      tag,            {.ui = ~0 } },
	{ MODKEY,                       XK_comma,  focusmon,       {.i = -1 } },
	{ MODKEY,                       XK_period, focusmon,       {.i = +1 } },
	{ MODKEY|ShiftMask,             XK_comma,  tagmon,         {.i = -1 } },
	{ MODKEY|ShiftMask,             XK_period, tagmon,         {.i = +1 } },
	TAGKEYS(                        XK_1,                      0)
	TAGKEYS(                        XK_2,                      1)
	TAGKEYS(                        XK_3,                      2)
	TAGKEYS(                        XK_4,                      3)
	TAGKEYS(                        XK_5,                      4)
	TAGKEYS(                        XK_6,                      5)
	TAGKEYS(                        XK_7,                      6)
	TAGKEYS(                        XK_8,                      7)
	TAGKEYS(                        XK_9,                      8)
	{ MODKEY|ShiftMask,             XK_q,      quit,           {0} },
	{ MODKEY,                       XK_z,      spawn,          {.v = slockcmd } },
	{ MODKEY,                       XK_x,      spawn,          {.v = firefoxcmd } },
	{ MODKEY,                       XK_q,      spawn,          {.v = powercmd } },
	{ 0,			XF86AudioPrev,		spawn,	   {.v = prevcmd } },
	{ 0,			XF86AudioNext,		spawn,	   {.v = nextcmd } },
	{ 0,			XF86AudioPlay,		spawn,	   {.v = playcmd } },
	{ 0,			XF86AudioMute,		spawn,	   {.v = mutecmd } },
	{ 0,			XF86AudioPrev,		spawn,	   {.v = prevcmd } },
	{ 0,			XF86AudioNext,		spawn,	   {.v = nextcmd } },
	{ 0,			XF86AudioLowerVolume,	spawn,	   {.v = lowercmd } },
	{ 0,			XF86AudioRaiseVolume,	spawn,	   {.v = raisecmd } },
};

/* button definitions */
/* click can be ClkTagBar, ClkLtSymbol, ClkStatusText, ClkWinTitle, ClkClientWin, or ClkRootWin */
static Button buttons[] = {
	/* click                event mask      button          function        argument */
	{ ClkLtSymbol,          0,              Button1,        setlayout,      {0} },
	{ ClkLtSymbol,          0,              Button3,        setlayout,      {.v = &layouts[2]} },
	{ ClkWinTitle,          0,              Button2,        zoom,           {0} },
	{ ClkStatusText,        0,              Button2,        spawn,          {.v = termcmd } },
	{ ClkClientWin,         MODKEY,         Button1,        movemouse,      {0} },
	{ ClkClientWin,         MODKEY,         Button2,        togglefloating, {0} },
	{ ClkClientWin,         MODKEY,         Button3,        resizemouse,    {0} },
	{ ClkTagBar,            0,              Button1,        view,           {0} },
	{ ClkTagBar,            0,              Button3,        toggleview,     {0} },
	{ ClkTagBar,            MODKEY,         Button1,        tag,            {0} },
	{ ClkTagBar,            MODKEY,         Button3,        toggletag,      {0} },
};

