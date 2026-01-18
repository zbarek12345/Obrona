# Unity
Unity to jeden z najpopularniejszych silników gier na świecie, używany do tworzenia gier 2D i 3D, aplikacji VR/AR/XR, symulacji oraz doświadczeń interaktywnych. W 2026 roku aktualną wersją jest **Unity 6** (z wydaniami LTS takimi jak 6.3), która wprowadza liczne usprawnienia w wydajności, grafice, multiplayerze i AI, przy zachowaniu klasycznych zalet silnika.


### Renderowanie i grafika
Unity oferuje trzy główne pipeline'y renderowania:
- **Universal Render Pipeline (URP)** — zoptymalizowany pod kątem wydajności na urządzeniach mobilnych i cross-platform, z silnymi optymalizacjami mobilnymi oraz wsparciem dla 6-kierunkowego oświetlenia.
- **High Definition Render Pipeline (HDRP)** — dla wysokiej wierności wizualnej, z zaawansowanymi efektami takimi jak volumetric fog, atmospheric scattering, realistyczna woda, lepsze renderowanie włosów i skóry.
- **Built-in Render Pipeline** — starszy, ale nadal wspierany.

Kluczowe nowości i cechy w Unity 6:
- GPU Resident Drawer — przenosi statyczne obiekty na GPU, znacząco redukując obciążenie CPU.
- GPU Occlusion Culling — eliminuje renderowanie niewidocznych obiektów.
- Spatial Temporal Post-Processing (STP) — temporal upscaling poprawiający jakość obrazu.
- Render Graph — zmniejsza zużycie pamięci nawet o 50% na urządzeniach mobilnych.
- Adaptive Probe Volumes (APV) — automatyzuje oświetlenie pośrednie.
- Produkcyjne ray tracing na PC, Xbox Series X|S i PlayStation 5.

### Multiplayer
Unity 6 wprowadza kompletne, end-to-end workflow multiplayerowe:
- Multiplayer Center — centralny hub z narzędziami i usługami.
- Multiplayer Widgets — gotowe szablony UI do lobby, czatu głosowego itp.
- Multiplayer Play Mode — testowanie wielu instancji gry w edytorze (do 4 klientów jednocześnie).
- Distributed Authority (Beta) w Netcode for GameObjects — skalowalna autorytetyzacja sieciowa.
- Integracja z Unity Gaming Services (Multiplay Hosting itp.).

### Sztuczna inteligencja (AI)
- Unity AI (Beta w 6.3 LTS) → kontekstowa pomoc w edytorze, automatyzacja zadań, generowanie assetów.
- Sentis → runtime AI pozwalający na uruchamianie modeli ONNX (np. z Hugging Face) bezpośrednio w grze – do inteligentnych przeciwników, animacji czy interakcji z kamerą/mikrofonem.

### Wsparcie platform
Unity wspiera ponad 20 platform docelowych, w tym:
- PC (Windows, macOS, Linux)
- Mobile (iOS, Android)
- Konsole (PlayStation, Xbox, Nintendo Switch)
- Web (WebGL, z nowymi optymalizacjami)
- VR/AR/XR (Quest, Vision Pro itp.)

Nowości w Unity 6:
- Lepsze wsparcie dla mobile web (uruchamianie gier Unity w przeglądarkach mobilnych)
- Zwiększony limit pamięci Web do 4 GB
- WebAssembly SIMD i multithreading C/C++
- Build Profiles — łatwe zarządzanie wieloma konfiguracjami buildów.

### Wydajność i stabilność
- Do 4× wyższa wydajność CPU dzięki nowym funkcjom.
- Lepsze profilowanie (Profiler Highlights, Memory Profiler).
- Poprawki w multithreadingu grafiki (DirectX12).
- Wszystkie wydania testowane w rzeczywistych produkcjach (Production Verification).

### Edytor i narzędzia produkcyjne
- Skryptowanie w **C#** (z Burst Compiler i Jobs System dla wysokiej wydajności).
- Zaawansowany edytor z Scene/Game view, Inspector, Hierarchy, Profiler.
- UI Toolkit — nowoczesny system UI z data binding.
- Cinemachine (kamery), Timeline (cutsceny), ProBuilder (prototypowanie 3D).
- Asset Store — ogromny ekosystem gotowych assetów, pluginów i narzędzi.
- Narzędzia 2D: Sprite Editor, Tilemap, 2D Physics.
- Fizyka: NVIDIA PhysX (3D) i Box2D (2D).
- Animacja: Animator, Mecanim, dopplerowane audio.

Unity pozostaje silnikiem przyjaznym zarówno dla indie deweloperów, jak i dużych studiów, dzięki łatwości prototypowania, ogromnej społeczności i ciągłym aktualizacjom skupionym na wydajności i stabilności.

### Unity 4 (wydany w 2012 roku)

Unity 4 był znaczącym krokiem naprzód w porównaniu do Unity 3, skupiając się na poprawie grafiki, animacji i narzędzi dla deweloperów mobilnych oraz konsolowych. Kluczowe nowości i cechy:

- **Mecanim** – zupełnie nowy system animacji z retargetingiem (przenoszeniem animacji między różnymi modelami postaci), blendingiem i state machine.
- **Wsparcie dla DirectX 11** – lepsze efekty oświetlenia, tessellation i wyższa jakość grafiki na PC.
- **Shuriken Particle System** – ulepszony system cząsteczek (już wprowadzony wcześniej, ale dopracowany).
- **NavMesh i pathfinding** – wbudowane narzędzia do nawigacji AI (automatyczne generowanie siatek nawigacyjnych).
- **Lepsze wsparcie mobilne** – optymalizacje dla Androida i iOS, w tym dynamiczne cienie i lepsze zarządzanie pamięcią.
- **Eksport na Adobe Flash** (później porzucony) oraz Linux.
- **Inne** – poprawki w fizyce (PhysX 3), lepsze narzędzia do deploymentu na konsole.

Unity 4 był popularny w erze wczesnych gier mobilnych i indie (np. wiele tytułów z tamtego okresu jak *Temple Run 2* czy wczesne wersje *Hearthstone*).

### Unity 5 (wydany w 2015 roku)

Unity 5 przyniósł rewolucję w jakości grafiki i dźwięku, czyniąc silnik bardziej profesjonalnym i konkurencyjnym wobec Unreal Engine. To jedna z największych aktualizacji w historii Unity. Kluczowe nowości i cechy:

- **Physically Based Rendering (PBR)** – realistyczne materiały i oświetlenie oparte na fizyce.
- **Real-time Global Illumination z Enlighten** – dynamiczne oświetlenie pośrednie w czasie rzeczywistym.
- **Reflection Probes** – realistyczne odbicia środowiska.
- **Nowy system audio** – Audio Mixer z efektami, reverb zones i spatial blending.
- **Lepsze narzędzia 2D** – ulepszony Sprite Editor, 2D Physics (Box2D) i Tilemap (w późniejszych patchach).
- **64-bitowy edytor** – lepsze zarządzanie pamięcią i stabilność.
- **WebGL export** – natywne uruchamianie gier w przeglądarkach bez wtyczek.
- **UNet (Unity Networking)** – nowy system multiplayer (później zastąpiony przez Netcode for GameObjects).
- **Unity Cloud Build** – chmurowe budowanie projektów.

Unity 5 umożliwił tworzenie gier o jakości AAA przez mniejsze studia (np. *Pillars of Eternity*, *Cities: Skylines*).

### Tabela porównawcza: Unity 4 vs Unity 5 vs Unity 6

| Kategoria              | Unity 4 (2012–2015)                          | Unity 5 (2015–2017)                                   | Unity 6 (2024–obecnie, z LTS 6.3)                          |
|-----------------------|----------------------------------------------|-----------------------------------------------------|-----------------------------------------------------------|
| **Renderowanie/Grafika** | Built-in renderer, DirectX 11, podstawowe cienie i oświetlenie | PBR, Real-time GI (Enlighten), Reflection Probes, Built-in renderer | URP/HDRP, Render Graph, GPU Resident Drawer, Spatial Temporal Post-Processing, produkcyjny ray tracing |
| **Animacja**          | Mecanim (retargeting, state machine)         | Mecanim + poprawki                                  | Mecanim + zaawansowane narzędzia (np. doppler audio, timeline) + AI-assisted animation |
| **Audio**             | Podstawowy mixer, spatial audio               | Nowy Audio Mixer, reverb zones, efekty               | Ulepszony mixer + integracja z AI i spatial audio         |
| **Fizyka**            | PhysX 3.x                                    | PhysX 3.x + poprawki 2D                              | PhysX + DOTS/ECS dla wysokiej wydajności                   |
| **Multiplayer**       | Podstawowy networking (stary system)         | UNet (HLAPI/LLAPI)                                   | Netcode for GameObjects, Distributed Authority, Multiplayer Center, integracja z Gaming Services |
| **AI/Nawigacja**      | NavMesh                                      | NavMesh + poprawki                                  | NavMesh + Unity AI (Beta), Sentis (runtime ONNX models)    |
| **Wydajność**         | Podstawowe optymalizacje mobilne             | 64-bit edytor, lepsze zarządzanie pamięcią          | Do 4× wyższa wydajność CPU/GPU, multithreading, Burst Compiler, Jobs System |
| **Platformy**         | PC, mobile, konsole, Flash, Linux            | + WebGL, lepsze mobile                              | Ponad 20 platform, ulepszone Web (WASM, multithreading), mobile web, XR |
| **Edytor/Narzędzia**  | Podstawowy edytor, Asset Store               | UI System (uGUI), Cloud Build                       | UI Toolkit, Build Profiles, Multiplayer Play Mode, zaawansowany Profiler |
| **Główne fokus**      | Animacja i DX11                              | Grafika AAA i audio                                 | Stabilność, wydajność, multiplayer, AI, cross-platform    |

Unity 4 i 5 to już historyczne wersje (nie wspierane od lat), używane głównie w legacy projektach. Unity 6 reprezentuje dojrzały, nowoczesny silnik z naciskiem na wydajność i skalowalność dla dużych produkcji. Przejście z 4 na 5 było przełomowe pod względem wizualnym, natomiast z 5 na 6 – ewolucyjne, skupione na optymalizacjach i nowych workflowach (np. SRP wprowadzone po Unity 5).

### Godot

Godot to darmowy, open-source'owy silnik gier 2D i 3D, rozwijany od 2014 roku przez społeczność (początkowo wewnętrznie w argentyńskim studiu OKAM). Jest licencjonowany na MIT, co oznacza pełną swobodę użytkowania, modyfikacji i dystrybucji – bez żadnych opłat royalty czy runtime fee. Silnik wyróżnia się lekkim edytorem, systemem scen opartym na węzłach (nodes), własnym językiem skryptowym GDScript (podobnym do Pythona) oraz wsparciem dla C# i C++ poprzez GDNative/GDExtension. Godot jest szczególnie popularny wśród indie deweloperów za prostotę, wydajność w 2D i brak korporacyjnych ograniczeń.

W styczniu 2026 aktualną linią jest Godot 4.x (z wersją 4.6 w release candidate), ale poniżej opisane zostały wersje od 2.

### Godot 2.x (20 14–2018, ostatnia stabilna 2.1.6)

Godot 2 był pierwszą publicznie dostępną gałęzią po otwarciu kodu źródłowego w 2014. To wersja skupiona głównie na 2D, z podstawowym wsparciem 3D, idealna dla prostych gier mobilnych i desktopowych.

Kluczowe cechy:
- **System scen i węzłów** – wszystko budowane hierarchicznie z węzłów (Node2D, Sprite, CollisionShape itp.), co ułatwia kompozycję obiektów.
- **GDScript** – nowy język skryptowy, prosty i szybki do prototypowania.
- **Silny fokus na 2D** – świetne narzędzia do sprite'ów, animacji (AnimationPlayer), tilemap, particle system (Particles2D), fizyka 2D.
- **Podstawowe 3D** – prosty renderer OpenGL, bez PBR, z podstawowym oświetleniem i cieniami.
- **Fizyka** – własny, customowy engine 2D/3D (nie Bullet).
- **Edytor** – nowy interfejs z filesystem dock, multiple scene editing, ulepszony code editor z podświetlaniem, debugger.
- **Eksport** – PC, mobile (Android/iOS), web (HTML5), podstawowe konsole.
- **Inne nowości w 2.0/2.1** – lepszy debugger, video RAM optymalizacje, nowy file dialog, poprawki w audio.

Godot 2 był używany do wielu klasycznych indie gier 2D (np. wczesne prototypy). To wersja lekka i stabilna, ale już mocno przestarzała – nie wspierana od lat.

### Godot 3.x (2018–2024, ostatnia stabilna 3.6)

Godot 3 to ogromny skok jakościowy, z prawie całkowicie przepisany core'em. Wersja 3.0 (2018) wprowadziła profesjonalne narzędzia 3D, czyniąc silnik konkurencyjnym dla większych produkcji.

Kluczowe cechy i nowości:
- **Nowy renderer 3D** – Physically Based Rendering (PBR), global illumination (GI probes), reflection probes, zaawansowane materiały i oświetlenie.
- **Fizyka** – integracja Bullet Physics (dużo dokładniejsza i stabilniejsza niż custom w Godot 2).
- **GDNative** – możliwość ładowania natywnych modułów w C/C++ bez rekompilacji silnika.
- **Typed GDScript** – opcjonalne typowanie dla lepszej wydajności i czytelności kodu.
- **Wsparcie Mono/C#** – pełna kompatybilność z C# (od 3.0+).
- **Ulepszenia 2D** – nowy TileSet editor, 2D lights/shadows, poprawiona fizyka 2D, hierarchical culling.
- **Audio** – zaawansowany bus system, efekty 3D.
- **Edytor** – revamped inspector, nowe narzędzia (np. revamped 2D editor), OpenGL ES 2.0/3.0 renderer (później Vulkan w Godot 4).
- **Inne** – improved asset pipeline, visual shader editor, lepszy eksport (w tym WebAssembly).

Godot 3 był szeroko używany do hitów indie jak *Cassette Beasts*, *Dome Keeper* czy portów. To wersja nadal stabilna dla legacy projektów, choć społeczność poleca migrację do 4.x.

### Godot 4.x (2023–obecnie, aktualna wersja: 4.6 RC1 na styczeń 2026)

Godot 4.x to największa rewolucja w historii silnika – prawie całkowicie przepisany core, z naciskiem na nowoczesną grafikę, wydajność i skalowalność. Wersja 4.0 wyszła w marcu 2023, a od tamtej pory gałąź rozwija się szybko (4.1, 4.2, 4.3 w 2024, a w 2026 zbliża się stabilna 4.6). Silnik pozostaje w pełni darmowy i open-source (licencja MIT), z ogromnym wkładem społeczności (tysiące commitów od setek contributorów).

Godot 4 czyni silnik konkurencyjnym nie tylko w 2D (gdzie zawsze był mocny), ale też w zaawansowanym 3D, przy zachowaniu lekkości (edytor ~100–200 MB, małe buildy). Kluczowe filozofie: system węzłów (nodes), sceny jako reusable komponenty, brak ukrytych opłat.

#### Renderowanie i grafika
- **Nowy renderer oparty na Vulkan** (z backendami Metal i Direct3D 12) – trzy metody:
    - **Forward+** (dla high-end PC/konsol): clustering lights, setki świateł dynamicznych bez kosztu.
    - **Mobile** (optymalizowany dla urządzeń mobilnych).
    - **Compatibility** (dla starszych urządzeń, kompatybilność z OpenGL).
- **Zaawansowane oświetlenie**:
    - SDFGI (Signed Distance Field Global Illumination) – dynamiczne GI w czasie rzeczywistym, bez bake'owania.
    - Voxel GI i lightmaps dla statycznego oświetlenia.
    - Volumetric fog, atmospheric effects, improved sky system.
- **Inne efekty**: Decals (naklejki na powierzchnie), occlusion culling, compositor effects (post-processing stacks), depth-based fog.
- Wysoka wierność wizualna zbliżona do AAA, ale z niskim overheadem – działa na integrated graphics.

#### Fizyka i nawigacja
- **Godot Physics** – nowy default engine 2D/3D (lepsza stabilność i dokładność niż w Godot 3).
- Opcjonalny **Jolt Physics** (dla jeszcze wyższej wydajności i precyzji w 3D).
- **NavigationServer** – unified nawigacja dla 2D i 3D (automatyczne pathfinding, avoidance agents).
- 2D physics interpolation dla płynniejszych ruchów.

#### Skryptowanie i rozszerzenia
- **GDScript 2.0** – ulepszone typowanie statyczne, lambdy, await/async, lepsza wydajność.
- **C# z .NET** – pełne wsparcie (desktop/mobile, web w planach).
- **GDExtension** – nowoczesna alternatywa dla GDNative: łatwe bindy w C++, Rust, Nim itp. bez rekompilacji silnika.
- Visual Scripting (wbudowany, ale mniej popularny).

#### Edytor i narzędzia produkcyjne
- **Revamped interfejs** – nowy theme, lepsze docking, multi-window editing (kilka scen jednocześnie).
- Zaawansowany script editor z autouzupełnianiem, debuggerem, live editing.
- **TileMap 2D** – warstwy jako oddzielne nodes, parallax, procedural generation, łatwiejsze malowanie.
- **3D tools** – import całych scen z Blendera (glTF), Movie Maker (renderowanie cutscenek), SkeletonModifier3D (IK, constraints).
- UI system – skalowalne GUI z anchors, containers.
- Audio – zaawansowane busy, 3D spatial audio.

#### Platformy i wydajność
- Eksport na: PC (Windows/macOS/Linux), mobile (Android/iOS), web (WebAssembly), konsole (przez third-party).
- Lepsze wsparcie XR (VR/AR).
- Multi-threaded core – lepsza wykorzystanie CPU, mniejsze buildy, wyższa FPS.
- Automatyczne optymalizacje (np. automatic engine update checks w nowszych wersjach).

#### Nowości w podwersjach 4.x (do 4.6 RC1)
- **4.2/4.3**: Premultiplied alpha, nowe compositor effects, TileMap layers as nodes, reverse Z buffer.
- **4.4+**: Pinned properties, live camera previews, dalsze optymalizacje wydajności.
- **4.6 (w trakcie)**: Kolejne bug fixy, stabilność i mniejsze feature'y przed ewentualnym Godot 5.

Godot 4 jest używany w dużych indie produkcjach (np. kontynuacje hitów z Godot 3) i zyskuje popularność po problemach Unity z opłatami.

### Ogólne porównanie Godot vs Unity

Godot i Unity to dwa popularne silniki dla indie i średnich produkcji, ale różnią się filozofią:

- **Licencja i koszty**: Godot – całkowicie darmowy, open-source (MIT), zero opłat. Unity – darmowy dla małych projektów, ale z subskrypcjami (Pro/Enterprise) i historycznymi kontrowersjami wokół runtime fee (2023–2024, później złagodzone).
- **Język skryptowy**: Godot – GDScript (łatwy, Python-like) + C#/C++. Unity – głównie C#.
- **Wydajność i lekkość**: Godot jest lżejszy (edytor ~100 MB, buildy mniejsze), lepiej zoptymalizowany dla 2D i mobile. Unity cięższy, ale skaluje się lepiej do dużych 3D projektów.
- **Grafika**: Unity (zwłaszcza HDRP w Unity 6) oferuje wyższą wierność wizualną (ray tracing, zaawansowane post-processing). Godot 4+ dogania (Vulkan, lepszy PBR), ale historycznie słabszy w high-end 3D.
- **Narzędzia i ekosystem**: Unity ma ogromny Asset Store, lepszą dokumentację i narzędzia (Cinemachine, Timeline). Godot ma wbudowane wszystko (bez potrzeby pluginów), ale mniejszy marketplace.
- **Społeczność i wsparcie**: Unity – większa, profesjonalne wsparcie konsolowe. Godot – szybko rosnąca (zwłaszcza po problemach Unity), ale mniej korporacyjna.
- **Multiplayer i zaawansowane funkcje**: Unity ma bardziej dojrzałe rozwiązania (Netcode, Gaming Services). Godot poprawia to w 4.x, ale prostsze.

### Tabela porównawcza: Godot 2.x vs 3.x vs 4.x vs Unity 6

| Kategoria              | Godot 2.x (2014–2018)                  | Godot 3.x (2018–2024)                        | Godot 4.x (2023–obecnie, 4.6 RC1)                  | Unity 6 (2024–obecnie)                              |
|------------------------|----------------------------------------|----------------------------------------------|----------------------------------------------------|----------------------------------------------------|
| **Renderowanie**      | Podstawowy OpenGL, brak PBR           | PBR, GI probes, OpenGL ES                     | Vulkan/Forward+, SDFGI, volumetric fog, decals     | URP/HDRP, Render Graph, ray tracing, STP           |
| **Fizyka**            | Custom engine                         | Bullet Physics                               | Godot Physics + Jolt (opcjonalnie)                  | PhysX + DOTS/ECS                                   |
| **Skryptowanie**      | GDScript                              | Typed GDScript + C# + GDNative                | GDScript 2.0 + C# (.NET) + GDExtension              | C#                                                 |
| **2D Narzędzia**      | Mocne (tilemap, particles)            | Bardzo mocne (nowy TileSet, 2D lights)       | Rewolucyjny TileMap (layers as nodes), parallax    | Dobre, ale mniej zintegrowane                      |
| **3D Narzędzia**      | Podstawowe                            | Profesjonalne (PBR, GI)                       | High-end (SDFGI, clustering, XR)                   | Zaawansowane (HDRP, GPU optimizations)             |
| **Multiplayer**       | Podstawowy                            | Podstawowy + extensions                      | Poprawiony (high-level API)                        | Zaawansowany (Netcode, Gaming Services)            |
| **Edytor**            | Lekki, nowy interfejs                 | Revamped inspector, visual shaders           | Multi-window, nowy design, live editing            | Zaawansowany (UI Toolkit, Profiler)                |
| **Licencja/Koszty**   | Darmowy, open-source (MIT)            | Darmowy, open-source (MIT)                   | Darmowy, open-source (MIT)                         | Darmowy/Pro, proprietary                           |
| **Wydajność**         | Dobra w 2D                            | Lepsza w 3D                                  | Multi-threaded, Vulkan, niskie wymagania           | Bardzo wysoka (GPU Resident Drawer, Burst)         |
| **Główne fokus**      | 2D, prostota                          | Zrównoważone 2D/3D                           | Nowoczesna grafika, skalowalność, otwartość        | Stabilność, multiplayer, AI, high-end produkcje    |

Godot 4.x to dojrzały silnik, idealny dla indie i średnich projektów – szczególnie jeśli cenisz wolność i lekkość. Unity 6 wygrywa w dużych, high-end 3D produkcjach z gotowymi narzędziami multiplayer/AI. Przejście z 3 na 4 wymaga migracji (niekompatybilne projekty), ale warto dla nowych możliwości.

### Unreal Engine 4 (2014–2022, ostatnia główna wersja 4.27)

Unreal Engine 4 był rewolucyjny w momencie premiery – przeszedł na model subskrypcyjny (później royalty 5% po przekroczeniu progu), oferując wysoką jakość grafiki AAA dla szerszego grona deweloperów. To silnik, na którym powstały hity jak *Fortnite*, *Gears of War 4*, *Final Fantasy VII Remake* czy wiele indie.

Kluczowe cechy:
- **Blueprint Visual Scripting** – system node-based bez kodowania, idealny dla designerów i prototypowania.
- **Physically Based Rendering (PBR)** – realistyczne materiały, dynamiczne oświetlenie, cienie.
- **Cascade Particle System** i **Niagara** (wprowadzone pod koniec UE4) – zaawansowane efekty cząsteczkowe.
- **Post-Process Effects** – bloom, DOF, motion blur, volumetric fog.
- **Animacja** – zaawansowany Animation Blueprint, retargeting, IK.
- **Fizyka** – NVIDIA PhysX, destrukcja (Chaos w późnych wersjach).
- **Multiplayer** – wbudowana replikacja, dedykowane serwery.
- **Platformy** – PC, konsole, mobile, VR.
- **Narzędzia** – Sequencer (cutsceny), Landscape tools, Persona (animacja).

UE4 był darmowy do pobrania, z royalty tylko od dużych sukcesów. Ostatnia wersja (4.27) jest nadal wspierana w niektórych projektach legacy.

### Unreal Engine 5 (2022–obecnie, aktualna wersja 5.7 z listopada 2025)

UE5 to ogromny skok, skupiony na next-gen grafice, otwartych światach i skalowalności. Premiera pełna w 2022, ale szybki rozwój – w styczniu 2026 aktualną jest **5.7** (wydana w listopadzie 2025), z naciskiem na lifelike worlds, open worlds i produkcyjną stabilność.

Kluczowe cechy i nowości (w tym z 5.4–5.7):
- **Nanite** – wirtualizowana geometria micropolygonów: miliony polygonów bez LOD-ów, import wysokiej szczegółowości mesh'y bezpośrednio z ZBrush/Blender.
- **Lumen** – dynamiczne global illumination i reflections w czasie rzeczywistym (bez bake'owania).
- **Chaos Physics** – zaawansowana destrukcja, pojazdy, ragdoll.
- **World Partition** – streaming ogromnych otwartych światów, Data Layers dla zarządzania.
- **MetaHuman Creator** – szybkie tworzenie realistycznych ludzi (extended w 5.7).
- **Niagara** – pełny system VFX, fluidy, modularne efekty.
- **Animation** – Control Rig, Motion Matching, modular rigging (nowości w 5.4+).
- **Rendering** – scalable high-fidelity (5.7), Temporal Super Resolution (TSR), Substrate materials.
- **Motion Design Mode** (z 5.4) – narzędzia do 2D motion graphics.
- **Procedural Content Generation (PCG)** – produkcyjne w nowszych wersjach.
- **Multiplayer i online** – integracja z Epic Online Services.
- **Platformy** – next-gen konsole, PC, mobile (z optymalizacjami), VR/AR.

UE5 jest używany w produkcjach jak *Fortnite Chapter 5*, *Senua's Saga: Hellblade II*, *Black Myth: Wukong*. Model biznesowy: darmowy, 5% royalty po $1M przychodu (z obniżką dla niektórych).

### Tabela porównawcza: Unreal Engine 4 vs Unreal Engine 5 vs Godot 4.x vs Unity 6

| Kategoria              | Unreal Engine 4 (2014–2022)                  | Unreal Engine 5 (2022–obecnie, 5.7)                  | Godot 4.x (2023–obecnie)                          | Unity 6 (2024–obecnie)                              |
|-----------------------|----------------------------------------------|-----------------------------------------------------|---------------------------------------------------|----------------------------------------------------|
| **Renderowanie/Grafika** | PBR, dynamiczne oświetlenie, post-effects    | Nanite, Lumen, TSR, Substrate, high-fidelity open worlds | Vulkan/Forward+, SDFGI, volumetric fog, decals    | URP/HDRP, Render Graph, ray tracing, STP           |
| **Fizyka/Destrukcja**  | PhysX, podstawowa destrukcja                | Chaos Physics, zaawansowana destrukcja              | Godot Physics + Jolt                              | PhysX + DOTS/ECS                                   |
| **Skryptowanie**      | C++ + Blueprints                            | C++ + Blueprints + Verse (nowy język)               | GDScript 2.0 + C# + GDExtension                    | C#                                                 |
| **Animacja**          | Animation Blueprint, retargeting            | Control Rig, Motion Matching, MetaHuman             | AnimationPlayer, Tween, Cutout                    | Mecanim + Timeline, AI-assisted                    |
| **Światy/Otwarte**     | Landscape, podstawowy streaming             | World Partition, Data Layers, PCG                   | Podstawowe (MultiMesh, procedural)                 | GPU Resident Drawer, Adaptive Probe Volumes        |
| **VFX/Cząsteczki**    | Cascade + Niagara (późno)                   | Niagara (pełne fluidy, modularne)                   | ParticleSystem (GPU/CPU)                          | VFX Graph                                          |
| **Multiplayer**       | Wbudowana replikacja                        | Epic Online Services, skalowalny                    | High-level API + extensions                       | Netcode, Distributed Authority, Gaming Services    |
| **Edytor/Narzędzia**  | Sequencer, Persona, Landscape               | Zaawansowany Sequencer, Motion Design, PCG          | Lekki, multi-window, wbudowane wszystko           | UI Toolkit, Profiler, Multiplayer Play Mode        |
| **Licencja/Koszty**   | Darmowy + 5% royalty                        | Darmowy + 5% royalty (po $1M)                        | Darmowy, open-source (MIT)                        | Darmowy/Pro, proprietary                           |
| **Wydajność/Skalowalność** | Dobra dla AAA                               | Next-gen, ogromne światy, mobile optymalizacje      | Lekki, multi-threaded, niskie wymagania           | Wysoka (4× CPU/GPU), mobilna                       |
| **Główne fokus**      | AAA grafika, Blueprints                     | Next-gen realism, open worlds, MetaHumans           | Otwartość, 2D/3D zrównoważone, prostota           | Stabilność, multiplayer, AI, cross-platform         |

Unreal Engine 5 (zwłaszcza 5.7) to lider w high-end 3D i realistycznej grafice AAA/next-gen, idealny dla dużych studiów. UE4 to solidna, sprawdzona baza dla starszych projektów. Godot 4.x wygrywa otwartością i lekkością (szczególnie 2D/indie), Unity 6 – wszechstronnością i ekosystemem dla mobile/cross-platform. Wybór zależy od skali: UE5 dla wizualnego spektaklu, Godot dla wolności, Unity dla szybkiego developmentu.