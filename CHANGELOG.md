# Changelog

All notable changes to UassetTranslator. Versions follow [Semantic Versioning](https://semver.org).

## 0.2.3 – 2026-10-23

- The license agreement (EULA 1.1) is final: no longer a draft. It is governed by the laws of Delaware, USA, and its
  list of Pro features now describes them in general terms (every command that creates, changes, builds, imports or
  validates assets or project files) instead of naming the commands of an early version. The software is unchanged.

## 0.2.2 – 2026-10-19

- Three ways to install, pick one: the one-line PowerShell command, `winget install TerraformEntertainment.UassetTranslator`,
  or the new `uasset-translator-0.2.2-setup.exe`. The installer needs no administrator rights: it installs for your
  Windows user, adds `uasset` to your PATH, appears in Settings > Apps with an uninstaller, and offers to add the
  Claude Code plugin when Claude Code is installed. It isn't code-signed yet, so Windows may show "Windows protected
  your PC": choose More info, then Run anyway.
- `uasset agents-md` finds its instructions when `uasset` runs through a link, as winget installs it.

## 0.2.1 – 2026-10-19

0.2.0 was never published; everything below since 0.1.0 is in 0.2.1.

- Bug reports: when a command fails in a way that looks like a bug, it says so and how to report it.
  `uasset bug-report ["what happened"]` writes a text file with the recent failed commands (the newest five are
  kept on this computer), the versions involved and the engine log's problems, to read and email to
  bugs@terraformentertainment.com. No license key and no asset contents go into it, and the tool sends nothing.
- The agent instructions say what to do when something fails: stop, tell the user plainly, offer a bug report, and
  never send anything; the list of what isn't supported yet is up to date.
- `uasset.exe` is now a native Windows program (compiled ahead of time): it starts faster and no longer unpacks a
  .NET runtime on first run.
- `validate` no longer reports the engine's shared cache server (ZenServer) starting slowly on a busy machine as a
  problem: that warning is about the computer, not the files.
- Readable graphs: `uasset layout` lays Blueprint graphs out for people to read (straight execution lines with pins
  level, further execution outputs below, data nodes to the left of what they feed in pin order, no overlaps, even
  spacing on the editor's grid, comment boxes refitted around their nodes), from node sizes measured against the
  editor's own. `uasset layout --check` (free) lists what breaks the rules: overlaps, bent or backwards wires,
  crossings, crowded or far-apart nodes, uncommented event chains, functions without a tooltip, oversized graphs.
  `uasset comment-box` wraps nodes in a padded comment box in a palette color by purpose (init, input, logic, error,
  network, feedback, debug, todo, neutral). Layout keeps comment boxes apart, and with a project it sizes nodes from the
  engine's display names of functions and parameters.
- A Cast node's Object input becomes an object pin when it is wired, as the editor makes it (it stayed a wildcard).
- New skills in the Claude Code plugin: `unreal-authoring` (the readability rules for every kind of asset: graph
  layout, comments and colors, naming and folders, materials, animation blueprints, behavior trees, widgets,
  Niagara, levels and more), `blueprint-cleanup`, `unreal-feature` and `unreal-mcp-authoring` (the same rules when
  working through an Unreal Editor MCP server). The AGENTS.md for other agents includes the rules.
- One-line install for other agents (Cursor, Codex, Antigravity, Copilot, Windsurf...): `irm
  https://github.com/terraform-entertainment/uasset-translator/releases/latest/download/install.ps1 | iex` installs
  `uasset.exe`, checks its checksum and puts it on the PATH; `uasset agents-md` writes the agent instructions into a
  project's AGENTS.md (running it again updates them).
- Licenses come from the Terraform Entertainment shop: `uasset activate <key>` activates a key bought on the product
  page (up to 2 computers per license), `uasset activate --offline` and `--code` activate without internet on this
  computer, and the 14-day trial starts with the first Pro command. Activation and the trial contact the license
  server once; licenses are then checked offline.
- Discover the engine (free): `uasset find` searches every Blueprint-usable class, function, event and property, and
  `uasset describe` explains one, with every pin, default and flag. The data comes from Unreal's own header tool,
  run against the project's engine and plugins, and is cached.
- Add nodes (Pro): `uasset add-node` adds calls to any Blueprint-callable function, variable get/set, branch,
  sequence, reroute, self, comments, events, custom events, casts, standard macros, spawn actor, create widget,
  construct object, subsystems, switches, select, arrays and math operators, make and break struct, calls of
  blueprint functions and custom events, interface messages, parent calls, event dispatchers (bind, unbind, call,
  assign, create event), component and widget events, Enhanced Input action events and key events, built from
  the engine's own metadata the way the editor builds it.
- `validate` accepts assets saved by older engine versions and older packages that do not record their name.
- Delete nodes (Pro): `uasset delete-node` removes a node, its wires and anything it owns.
- Add variables (Pro): `uasset add-variable` adds a member variable of any type (basic types, structs, enums,
  object and class references, soft references, interfaces, arrays, sets and maps), saved exactly as the editor saves
  it. `props` shows variable types by name.
- Variable settings (Pro): `uasset variable` changes everything in a variable's Details panel: category, tooltip,
  instance editable, read only, expose on spawn, private, replication and its condition, slider and value ranges,
  units, bitmask, config, transient, save game, advanced display, deprecation, and any metadata. `show` lists them.
- Add functions (Pro): `uasset add-function` adds a function with inputs and outputs, as the editor makes it.
- Rename and delete functions and add or remove their inputs and outputs (Pro): `uasset function <file> <F>
  name|delete|add-input|add-output|remove-param`, with their calls rebuilt here and renamed in other blueprints.
- Local variables (Pro): `uasset local` adds, renames, retypes, deletes and sets the default of a function's local
  variables; `add-node get|set` inside the function reads and writes them.
- Custom events (Pro): `uasset event` adds and removes parameters, renames, and sets replication (multicast, server,
  client, reliable) and call in editor; functions take the same replication settings. `show` lists them.
- `uasset state <file> <Node> enabled|disabled|dev-only` enables and disables nodes, and converts casts to pure or impure.
- `copy-node --to <Graph>` copies a node into another graph, `--from <blueprint>` from another blueprint.
- Batch files name the nodes they add (`add-node ... as b`) and refer to them later as `$b`.
- Widget blueprints (Pro): `uasset widget` adds widgets (any UMG widget or a widget blueprint) to panels, deletes
  them with their children, moves them between panels, renames them (Get nodes follow), and sets their properties
  and their slot layout (padding, alignment, canvas position and size), saved as the designer saves them, with the
  compiled widget tree and widget variables kept in step. `add-node get` reads widget variables.
- More nodes (Pro): `add-node` makes Format Text (one input per {argument}, kept in step when the format changes),
  Make Set, Make Map, MultiGate, Do Once MultiInput, class casts, enum literals, Byte to Enum, For Each in Enum,
  enum counts and names, Async Load Asset and Class, Get Data Table Row, Get Class Defaults, Ease, and legacy input
  axis, action and touch events. `pin add|remove` works on MultiGate and Make Map; wires type Make Map and Format
  Text inputs.
- Inherited components (Pro): `uasset component <file> <Component> set <Property> <value>` changes a component a
  parent blueprint adds, as the child's Details panel does (an override saved with only what differs from the
  parent); `reset` puts it back, and an override that changes nothing is removed. `set`/`reset` work on the
  blueprint's own components too. `show` lists the overrides under "inherited components".
- Materials (Pro): `uasset material-node <material> <Node> delete | move <x> <y>` deletes a node (its wires go with
  it) or moves it; `uasset material-comment` adds comment boxes, saved as the material editor saves them.
- Input mapping contexts (Pro): `show` lists their key mappings with triggers and modifiers; `uasset input` maps keys
  to actions, changes or removes mappings, and adds, changes and removes triggers (Pressed, Hold, Tap...) and
  modifiers (Negate, SwizzleAxis, DeadZone...), saved as the editor saves them.
- Curves (Pro): `show` lists the keys of float, vector and linear color curves; `uasset curve` adds, moves,
  changes and deletes keys (constant, linear or cubic), with tangents set as the curve editor sets them.
- Levels (free): `show` lists a map's actors (class, label, folder, saved properties) and their components.
- Levels (Pro): `uasset create level` makes an empty level; `uasset level` places actors as the editor does (lights,
  sky and fog, cameras, player starts, triggers, static mesh actors, volumes...), copies placed actors within a level
  or from another one, deletes them, and moves, rotates, scales, labels and files them in folders. `set` reaches an
  actor's components by label (Lamp.LightComponent0:Intensity). Duplicating a level gives its actors new GUIDs.
- Levels (Pro): `level add` places actors of the project's blueprint classes too, built from the blueprint as the
  editor's construction builds them: native components, construction script components (attached, with child
  blueprints' overrides) and timelines.
- Level blueprints: `show` on a map lists its level blueprint after its actors, and every blueprint command (nodes,
  wires, pins, variables, functions, events, timelines...) edits it as it edits any blueprint.
- Collapse and expand (Pro): `uasset graph <file> <Graph> collapse graph|function|macro <Node>...` collapses nodes
  into a collapsed graph, a new function or a new macro, with the wires passing through its pins, as the editor's
  Collapse Nodes, Collapse to Function and Collapse to Macro do; `expand <Node>` expands a collapsed graph, a macro
  instance or a call of one of the blueprint's functions back into the graph.
- Macros made by `macro add` no longer save the editable flag their tunnels have by default.
- Node titles (Pro): `uasset title <file> <Node> <New title>` renames what a node's title shows, as typing on it
  does: a comment box's text, a custom event, a collapsed graph, a function, or a timeline (with its variable, its
  functions and its tracks' properties).
- Duplicating a blueprint renames the category the compiler gives its timeline variables.
- Math operators take mixed types as in the editor: wiring a Vector and a float into Multiply, or an int and a double
  into Add or Greater, picks the function the editor picks (its type promotion) and keeps each pin's wired type when
  it converts; such wires are no longer refused.
- `set` creates color (FColor) properties that keep their default, and shows them as the editor writes them.
- `add-node <file> <Graph> set-members <Struct> [<Member>...]` (Pro) adds Set Members in a struct, with the members
  named shown as inputs, as the editor places it and ticks them.
- Make and Break Struct of blueprint structs: members without a description have the empty tooltip the editor gives
  them (they used to get their name).
- New members of a blueprint enum type in a struct start at the enum's first entry, as in the editor (they were None,
  which the engine rejects).
- `validate` copies the project assets the files use (structs, enums, other blueprints...) into its scratch project, so
  they load without being listed.
- `add-node <file> <Graph> macro <Library>.<Macro>` (Pro) places a macro of a project macro library, for blueprints
  whose parent class the library allows, as the editor does.
- New assets of every Add menu type (Pro): `create asset --parent <Class>` makes the asset the editor's factory
  makes for about 136 engine classes (sounds, physics, foliage, render targets, curve tables, media, Paper2D,
  sequences, Niagara emitters, PCG graphs...), each compared with the editor's and loaded by the engine; classes that
  need another command or the factory's options say so.
- Animation layers (Pro): `create anim-layer-interface`, `anim ... layer add` (an interface's layers or a blueprint's own),
  `anim ... implement <ALI>` (the interface's layer graphs, as Class Settings adds them) and Linked Anim Layer nodes
  (`anim ... add AnimGraph LinkedAnimLayer:<Layer>`) set up as the palette's layer entries set them up, with a pin per
  input pose the layer takes (`anim ... add <Layer> LinkedInputPose`). Linked Anim Graph nodes run another animation
  blueprint (`LinkedAnimGraph:<ABP>`), and `anim ... transition ... blend custom` gives a transition its custom blend graph.
- Animation blueprint editing (Pro): `anim` places any animation node of the palette (sequence and blend space
  players, state machines, slots, cached poses, blends, IK...), states, conduits, aliases, the entry and transitions,
  deletes states (with their transitions) and transitions, as the editor's graph
  actions make them; poses link with `link`, node settings change with `set` and rules are built in the transition's
  graph with the blueprint commands. `create anim-blueprint <file> --skeleton <Skeleton>` makes a new one.
- Animation blueprints: `show` reads them as the editor draws them: each state machine with its entry, states,
  conduits, aliases (and the states they cover) and transitions with their settings; state graphs and transition rules
  named by their machine ("Locomotion/Idle", "Locomotion/Idle -> Walk / Run"); animation nodes titled by what they play
  (Sequence Player MM_Idle, Slot 'DefaultSlot', Use cached pose 'Locomotion') with their settings.
- Reimport: `uasset reimport <asset> [<file>]` updates a texture or a sound from its source file (or another one),
  keeping its settings, as the editor's Reimport does.
- EXR images: `uasset import` takes OpenEXR files (uncompressed, RLE, ZIP, PIZ and PXR24; half or float; any channel
  names) as HDR textures, exactly as the editor decodes them.
- Animation notifies: `uasset notify <anim> add` adds named notifies (Animation Blueprint events such as footsteps),
  notify objects (play a sound, an effect, a Blueprint notify) and notify states with a duration, as the editor's
  notify panel adds them, and sync markers (`notify <anim> marker add`); `delete` removes one, and `show` lists them.
- Packages imported through Interchange (glTF, OBJ, textures) can now have objects removed, and `show --all` names
  their source file.
- Skeleton sockets: `uasset mesh <skeleton> socket add <Name> --bone <Bone>` adds an attach point on a bone (for weapons,
  effects, attached actors) as the skeleton tree does; `show` lists a skeleton's sockets.
- Virtual bones: `uasset mesh <skeleton> virtual-bone add <Source> <Target> [--name "VB Name"]` adds a bone that
  follows one bone in the space of another (for IK targets), and `virtual-bone <Name> delete` removes one, as the
  skeleton tree does; `show` lists them.
- Mesh-only sockets: `uasset mesh <skeletal mesh> socket add <Name> --bone <Bone>` adds a socket to that one mesh
  (the skeleton tree's Create Mesh Socket); one named like a skeleton socket overrides it for that mesh.
- Morph targets: a skinned glTF's morph targets (blend shapes) are imported with the skeletal mesh as the editor imports
  them, each with a curve of the same name on the skeleton so animations can drive it; `show` lists them.
- Skeletal mesh imports keep degenerate triangles and save the bounds as the editor's import does.
- Skeletal mesh LODs: `uasset mesh <skeletal mesh> lods <count>` adds or removes levels of detail as the editor's LOD
  settings regenerate them (25% of the triangles, then half of that each level); the engine reduces them when it next
  loads the mesh.
- IK Rigs: `uasset create ik-rig <new file> [--mesh <SkeletalMesh>]` and `uasset ikrig <rig> mesh | retarget-root |
  goal add | chain add | solver add | solver <n> start|goal` build an IK Rig as the IK Rig editor does (the mesh's
  skeleton copied in bit for bit, retarget chains for retargeting, Full Body IK solvers with their goals); `show` lists
  bones, chains, goals and solvers. Instanced struct values (such as a rig's solvers) now read as `/Script/Module.Struct(...)`
  and save without losing their end marker.
- IK Retargeters: `uasset create ik-retargeter <new file> [--source <IKRig>] [--target <IKRig>]` and `uasset retargeter
  <rtg> source|target <IKRig> | ops default | map-chains exact|fuzzy|clear` set up a retargeter as the IK Retargeter
  editor does: the two rigs and their preview meshes, the default op stack (pelvis motion, FK chains, run IK rig, root
  motion, curve remap) and each target chain's source chain; `show` lists the rigs, ops and chain maps.
- Control Rigs: `show` lists a Control Rig's hierarchy (bones, controls, nulls... as a tree), read with the Oodle
  library of the installed Unreal Engine. `uasset create control-rig <new file>` and `uasset controlrig <rig> mesh |
  refresh <SkeletalMesh> | control add | null add | bone add [--on <Element>]` set the preview mesh, bring in the
  mesh skeleton's bones and add items as the hierarchy panel does.
- Batch retargeting: `uasset retarget <IKRetargeter> <Animation>... [--to <folder>] [--prefix|--suffix <text>]` makes
  copies of animations on another character with an IK Retargeter. The tool runs the installed Unreal Engine
  headless (no window) on copies, as `validate` does, and adds only the new animations to the project; nothing
  there is overwritten.
- Fixed: assets imported from FBX (and Alembic or USD) now read their import record (where the source file came
  from), which stayed unread before; such assets (Epic's mannequin animations) show and edit fully.
- Level sequences: `sequence <LS> bind <map> <Actor>` binds a level actor as Add Actor to Sequencer does (a static
  mesh actor with its transform track starting at its transform), `sequence <LS> <Binding> track transform` adds a
  transform track, and `sequence <LS> <Binding> key <frame> Location.X=500 Rotation.Z=90` sets keys with Sequencer's
  auto tangents; `show` lists a sequence's bindings, tracks and keys.
- Level sequences: cameras. Binding a Camera Actor or Cine Camera Actor adds, as Sequencer does, a binding for its
  camera component (`Cam.CameraComponent`) with the lens's property tracks (focal length, focus distance and aperture;
  field of view) keyed at their current values, and a camera cut to the camera when the sequence has none.
  `sequence <LS> Cam.CameraComponent key 30 CurrentFocalLength=50` keys a property track; `show` lists the camera
  cuts and property tracks.
- Level sequences: lights. Binding a point, spot, rect or directional light adds, as Sequencer does, a binding for its
  light component with an intensity track keyed at its intensity and a color track starting at its color.
  `sequence <LS> Lamp.LightComponent0 key 30 Intensity=8000 LightColor.R=0.25` keys them (a color by its channels R,
  G, B, A, in linear space).
- Level sequences: skeletal meshes. Binding a skeletal mesh actor adds its transform track and an animation track, as
  Sequencer does, and `sequence <LS> <Binding> animation <Anim> [<frame>]` adds an animation to it (as the track's
  + Animation menu does: on the next row, as long as the animation plays). A mesh with a default animating rig (such
  as Epic's mannequins), for which Sequencer also adds a Control Rig track, is not supported yet.
- Level sequences made by the tool now list the same imports as the editor's (the default objects Unreal saves with
  each track and section).
- Level sequences: camera cuts. `sequence <LS> cut <Camera> [<frame>]` cuts to a camera from a frame, as the camera
  cut track's + Camera does: the cut lasts until the next cut or the end, the previous cut now ends where it starts,
  and a cut at the same place changes its camera. `show` lists the cuts in order.
- Fixed: bindings added to a level sequence are now kept in the order Unreal keeps them (by their ids), and a second
  binding with the same name (two cameras' CameraComponent) gets the next sorting order, as in Sequencer.
- Level sequences: fades and sounds. `sequence <LS> fade <frame> <value>` keys the fade track (0 clear, 1 black),
  adding it first as + Track > Fade Track does; `sequence <LS> audio <Sound> [<frame>]` adds a sound wave or cue to
  the audio track as its + Audio does (as long as the sound plays, one second for a looping one; on the first row
  where it fits). `show` lists the fade keys and the sounds.
- See a level sequence: `render <LS> --frame <n>` plays the sequence on its level to that frame in the installed
  engine (headless) and takes the picture through the camera its camera cut shows there (`--level` names the level
  when its bindings don't).
- Fixed: `sequence <LS> bind` found a copied map by the name it was saved under instead of where it is now.
- Level sequences: deleting, as Sequencer deletes. `sequence <LS> <Binding> delete` (with its component bindings),
  `sequence <LS> <Binding> track <Track> delete` (Transform, Animation, or a property such as FieldOfView),
  `sequence <LS> track Fade|Audio|CameraCut delete`, `sequence <LS> <Binding> delete-key <frame> <Channel>...` and
  `sequence <LS> fade <frame> delete`. What nothing uses any more leaves the file, as the editor's save leaves it out.
- Level sequences list their soft references (the bound actors and their classes) in the order Unreal saves them.
- Navigation: `build-navigation <map>` builds the level's navmesh as Build > Build Paths does, in the installed engine
  (headless, on copies): inside its Nav Mesh Bounds Volumes (`level <map> add NavMeshBoundsVolume --scale ...`), and
  reports whether each volume's centre is on the navmesh. The level comes back with its RecastNavMesh, the old one
  backed up; AI Move To works at once.
- Fixed: `duplicate` failed on levels with a level blueprint (its last edited graph is a soft path the copy renames;
  the package's table of soft paths was left with the old name).
- Scripted input: `play <map> --input "1 IA_Jump; 2 IA_Move 1,0 for 1.5; 3 key:SpaceBar"` (or a file with one step
  per line) plays the level in the editor, headless, and presses Enhanced Input actions or keys at those seconds (for
  0.2 s, or as long as given), as if a player did; what blueprints printed and the runtime errors come back. A line
  printed every frame while an input is held is shown once with its count.
- Inspecting a running game: the play script (`--script`, which `--input` still names) also takes
  `exec <console command>`, `read <Actor>.<Property>` (an actor by label, or `player` for the player's pawn; Location,
  Rotation and Velocity too) and `shot [<name>]` (a picture of the game view) steps: `play <map> --script "2 read
  player.Location; 2 shot; 3 read BP_Door.bIsOpen"`. The values read are listed with their times.
- Play scripts can call functions and custom events while the game runs: `call <Actor>.<Function> [<argument>...]`
  (`level` for the level blueprint, `player` for the player's pawn; arguments are numbers, true/false, text, or x,y,z
  vectors); what it returns is listed with the values read.
- Play scripts can show a widget blueprint while the game runs: `widget <WidgetBlueprint>` (Create Widget, Add to
  Viewport), so its Construct logic runs and what it prints or breaks is reported. Pictures (`shot`) show the scene
  without widgets.
- Functional tests written as blueprints: `create blueprint BP_CoinTest --parent FunctionalTest` is the editor's (its
  billboard, rendering and name components; Prepare Test, Start Test and Tick events); its Start Test calls
  `self.FinishTest` (a node kind that now reaches functions a blueprint inherits from engine classes); placed with
  `level <map> add BP_CoinTest CoinTest`, it shows its label as the editor does and the map lists it, so `test <project>
  "Project.Functional Tests"` runs it and reports its result and message.
- Navigation links: `level <map> add NavLinkProxy` places a Nav Link Proxy as the editor does, its link ids made as
  the engine makes them (from the component's path and the actor's GUID); move its link points with `set`. With
  NavModifierVolume (its AreaClass) and the navmesh's agent and cell sizes in `settings <project> RecastNavMesh`,
  `build-navigation` builds what AI can walk.
- `render <LS> --frames 0-90/15` (or `--frames 0,30,60`) renders several frames of a sequence in one engine session, a
  picture each (`<name>_<frame>.png`) with the camera it was seen through.
- Blueprints of actor classes that bring components of their own (StaticMeshActor, DefaultPawn, PlayerCameraManager,
  TriggerBox...) are now made by the editor's Blueprint factory in the installed engine (headless, about 20 s), so
  they get exactly the editor's components and events; before, they got a scene root of their own and the editor
  replaced it on the next save.
- Niagara systems from the engine's templates: `create niagara-system NS_Fire --template FountainLightweight` (also
  RadialBurst, DirectionalBurst, SimpleExplosion, MinimalLightweight...), as the asset wizard makes them; place one with
  `level <map> add NiagaraActor` and set its NiagaraComponent0's Asset. The editor recompiles its scripts when it loads it.
- Pictures in play scripts are requested again when the game view drops a request, and play waits for them.
- Smart objects (the SmartObjects plugin): `create asset SO_Bench --parent SmartObjectDefinition` makes a definition as
  the editor does, `array SO_Bench Slots insert "()"` adds a slot (with its own id and conditions setup, as the slot
  list's + does), and `set SO_Bench Slots[0].Offset (X=0,Y=-50,Z=0)` places it (also Rotation, Name, ActivityTags...).
  `show` lists the slots. Single-precision rotations (Rotator3f) are now read and set.
- State trees (the StateTree and GameplayStateTree plugins): `create state-tree ST_Guard --schema AI` (or Component)
  makes one as the editor's factory does; `state-tree ST_Guard add-state Patrol [--parent <State>]` adds states,
  `state-tree ST_Guard Patrol task Delay` and `... condition Random` add tasks and enter conditions,
  `state-tree ST_Guard Patrol transition --to Chase [--on Succeeded]` adds transitions, and
  `state-tree ST_Guard Patrol set Tasks[0].Duration 2.5` changes a task's settings, and
  `state-tree ST_Guard Patrol bind EnterConditions[0].Left Actor.CustomTimeDilation` feeds an input from the Actor or
  AIController context (or a property of it). `state-tree ST_Guard Chase delete` deletes a state (and those under it),
  `state-tree ST_Guard Patrol remove Tasks[0]` a task, condition or transition, with the bindings that relied on
  them. `state-tree ST_Guard global-task DebugText` and `evaluator <Evaluator>` add the tree's own tasks and
  evaluators; `state-tree ST_Guard Idle transition-condition 0 Random` puts a condition on a transition. `show` draws
  the tree with its bindings. The editor
  compiles the tree when it loads it. `set` can now reach the fields inside instanced structs. To run one, give an AI
  controller blueprint the component (`add-component BP_GuardAI StateTreeAIComponent StateTree`) and point it at the
  tree (`component BP_GuardAI StateTree set StateTreeRef.StateTree /Game/AI/ST_Guard.ST_Guard`).
- Fixed: `component <bp> <Component> set` saved a value even when it equalled the component class's default; like
  the editor, it now saves nothing then.
- Widgets of a widget class: `create widget WBP_Menu --parent CommonActivatableWidget` (or CommonButtonBase, any
  UserWidget class or widget blueprint) makes a widget blueprint of that parent, as the Widget Blueprint factory does
  when a parent is picked. Fixed: `create blueprint --parent` with a widget class made a plain blueprint instead of a
  widget blueprint; it now makes the widget blueprint. Common UI style blueprints (CommonTextStyle,
  CommonButtonStyle) are made as the editor makes them. Common UI's palette widgets (CommonTextBlock, CommonBorder,
  CommonLazyImage, CommonListView, the switchers...) are placed with `widget <file> add` as the palette makes them.
- MetaSounds: `show` draws a MetaSound's graph (nodes, input defaults, connections). `metasound MS_Tone add Sine.Audio
  at 300 100` adds a node of any of the engine's 800 node classes (`metasound classes Sine` finds them),
  `metasound MS_Tone Sine set Frequency 440` sets an input, and `metasound MS_Tone connect Sine.Audio
  UE.OutputFormat.Mono.Audio:0` wires it, as the editor's MetaSound builder does. `metasound MS_Tone add-input Pitch
  Float 220` adds a graph input (a control the game can set), `metasound MS_Tone disconnect Sine.Frequency` removes a
  wire, and `metasound MS_Tone Sine delete` a node (with its wires).
- Fixed: MetaSounds made with `create asset --parent MetaSoundSource` (or MetaSoundPatch) all had the same internal
  class name and author, so the engine could mix them up; each now gets its own, and the author is the user.
- MetaSounds: `metasound MS_X add-output Level Float` adds a graph output, `add-variable Freq Float 330` a variable,
  and `add-get Freq`, `add-set Freq` and `add-get-delayed Freq` its nodes, wired into the variable's chain as the
  editor wires them. MetaSound patches (`create asset --parent MetaSoundPatch`) can be built from empty, and another
  sound uses one as a node: `metasound MS_X add MSP_Osc at 300 100`. `show` lists the variables, and names nodes that
  share a name (such as variable nodes) by their #index.
- Fixed: MetaSound patches made with `create asset` still shared one internal class name (the fix above missed them,
  as a patch stores its graph under a differently spelled name).
- MetaSound presets (a sound that reuses another's graph with its own input values): `metasound MS_Quiet preset-of
  MS_Tone` makes one, rebuilt from the parent exactly as the editor builds it; `metasound MS_Quiet default Volume 0.2`
  sets an input's value (on a preset, overriding the parent's), `default Volume inherit` takes the parent's again, and
  `metasound MS_Quiet rebuild` refreshes a preset after its parent changed. `show` names a preset's parent and marks
  each input's default as its own or inherited. `default` also sets the defaults of an ordinary MetaSound's inputs.
- Foliage: `uasset foliage L_Forest.umap scatter FT_Tree --area -5000 -5000 5000 5000 --count 300 --spacing 200`
  scatters trees over an area, dropped onto the ground below and placed with the foliage type's own settings (scale
  range, random rotation, aligning to slopes, slope and height limits), the way the foliage paint tool places them;
  `foliage <map> add FT_Rock 100 200 0` puts one at a point (or many from a CSV file), and `foliage <map> clear FT_Tree`
  removes them. The installed engine does the painting headless (about 25 seconds), so the result is exactly the
  editor's; World Partition levels work too. Foliage types made with `create asset --parent
  FoliageType_InstancedStaticMesh` now get their mesh bounds when their Mesh is set, as in the editor.
- Safety: the jobs that let the engine rebuild a level (`build-navigation`, `build-lighting`, `foliage`) now refuse to
  copy the result back when the engine dropped any of the level's actors (it does when it cannot load their class,
  such as a C++ class of the game's own code), instead of replacing the level without them.
- Fixed: struct fields the engine declares as world-coordinate doubles (a bounds' SphereRadius...) were saved with a
  type name the engine does not use, so they could not be read back.
- See your menus: `uasset render WBP_MainMenu.uasset` draws a widget blueprint as the game draws it and saves a PNG
  (about 20 seconds, the installed engine headless). It fills 1280 x 720 like a full-screen menu (`--size` for
  another), or `--desired-size` draws it at the size it asks for, and `--animation FadeIn --time 0.5` shows it half a
  second into one of its animations.
- MetaSounds: `metasound MS_X Pitch delete` removes a graph input or output with its node, `remove-variable Freq` a
  variable with all its nodes (the chain rejoined as the editor rejoins it), and `rename Pitch Tone` renames an input,
  output or variable. Fixed: deleting nodes and wires kept the remaining ones in a different order than the editor
  does (the editor moves the last one into the gap), which the engine accepted but the editor would have saved
  differently.
- PCG graphs (procedural content): make one with `create asset Content/PCG/PCG_Forest.uasset --parent PCGGraph`,
  then `pcg PCG_Forest.uasset add SurfaceSampler at 300 0`, `pcg PCG_Forest.uasset add StaticMeshSpawner at 600 0`,
  `pcg PCG_Forest.uasset connect Input.In SurfaceSampler_0.Surface` (and on to the spawner and `Output.Out`), and
  `pcg PCG_Forest.uasset SurfaceSampler_0 set PointsPerSquaredMeter 0.2`. A spawner's meshes: `pcg PCG_Forest.uasset
  StaticMeshSpawner_0 set MeshSelectorParameters.MeshEntries "[(Descriptor=(StaticMesh=/Engine/BasicShapes/Cone.Cone),Weight=1)]"`.
  `move`, `delete` and `disconnect` work too; all 208 node types of the editor's palette can be added (`pcg types
  sampler` finds them, free), each made exactly as the graph editor makes it. `show` lists a graph's nodes, their
  settings and wires.
- PCG in levels: `pcg L_Forest.umap place PCG_Forest --at 0 0 0 --size 5000 5000 1000` puts a PCG volume with the
  graph in the level and generates it, `pcg L_Forest.umap generate` generates the level's PCG volumes again (or one,
  by name), and `pcg L_Forest.umap clear` removes what they generated. The installed engine does it headless (under a
  minute), so the result is exactly the editor's; World Partition levels work too. It reports how many meshes
  each volume made.
- Data layers in World Partition levels: `create asset Content/DL/DL_Night.uasset --parent DataLayerAsset` makes a
  data layer asset (with the colour the editor would give it), `level L_World.umap data-layer add DL_Night Activated`
  gives the level a layer of it that starts activated, `level L_World.umap Lamp data-layer add DL_Night` puts an actor
  in it (`remove` takes it out), `data-layer DL_Night state Loaded` changes how it starts, `data-layer DL_Night delete`
  removes it, and `level L_World.umap data-layer` lists the layers with their actors. Saved exactly as the Data Layers
  Outliner saves them, so the editor and World Partition see them at once.
- See a whole cutscene at once: `render LS_Intro.uasset --frames 0-150/30 --sheet` also puts every rendered frame into
  one picture (`LS_Intro_sheet.png`), left to right, then down.
- Spawnables in cutscenes: `sequence LS_Intro spawn CineCameraActor --at 0 -500 200` adds a camera the cutscene
  spawns itself (with its lens tracks and a camera cut), `spawn PointLight` a light, `spawn BP_Dragon Dragon` a
  blueprint actor, and `spawn L_Map.umap Rock` a copy of a level's actor; they appear only while the sequence plays and
  need nothing placed in the level. Key them like any binding. Saved as Sequencer's Add Actor saves them.
- Films made of shots: `sequence LS_Film shot LS_Intro`, then `shot LS_Chase` (placed after the last shot), and
  `sequence LS_Film range 0 300` to make the film as long as its shots; `subsequence LS_Crowd 30` plays another
  sequence from frame 30 on the Subsequences track. `show` lists them, and `render LS_Film --frames ...` sees each
  frame through the camera of the shot playing then.
- Hide and show actors in cutscenes: `sequence LS_Intro Door show 0`, then `sequence LS_Intro Door hide 90` makes the
  door vanish at frame 90 (a key on its visibility track, as keying Actor Hidden In Game in the Details panel does).
- Animate more in cutscenes: any animatable number on a bound actor or component can now be keyed, not only the
  default tracks: `sequence LS_Intro Lamp.LightComponent0 key 60 AttenuationRadius=2500` makes the track on the first key.
- Camera rigs: `level L_Set.umap add CameraRig_Rail` (and `CameraRig_Crane`) places them, and `sequence LS_Intro spawn
  CameraRig_Crane` gives a cutscene its own. `level <map> add PCGVolume` places a PCG volume without the engine; give
  it a graph with `set <map> "PCGVolume_0.PCG Component.PCGGraphInstance:Graph" /Game/PCG/PCG_Forest.PCG_Forest`, then
  `pcg <map> generate`.
- Fixed: copying or placing some actors (a rail camera rig's spline, among others) wrote their components 4 bytes short,
  and the engine refused the level.
- Particle effects: `show NS_Burst.uasset` lists each emitter's modules and their input values (lifetime, color,
  size, gravity, spawn counts...), and `niagara NS_Burst set OmnidirectionalBurst.InitializeParticle.Color
  "(R=1,G=0,B=0,A=1)"` changes one, as typing it in the Niagara editor's stack does (no recompile needed).
- Lightweight particle effects (the "Lightweight" templates): `niagara NS_Fountain set Fountain.InitializeParticle.Lifetime
  3`, a range `1.4..1.75`, or per channel `Color (1,0,0,1)`, as the details panel sets them; also the emitter's
  spawn rate (`Fountain.Spawn.Rate 300`) and loop duration (`Fountain.Emitter.LoopDuration 2`).
- Particle effects, static inputs: `niagara NS_Burst set OmnidirectionalBurst.ShapeLocation.Shape Primitive Cylinder`
  sets a module's static switch (`show` lists them, with each choice's name) or static input, as the stack does; the
  editor compiles the effect again when it next loads, saves or cooks it (the tool never needs to compile).
- Lightweight particle effects vary over a particle's life: `niagara NS_Fountain set Fountain.ScaleColor.Scale
  "gradient(0:(1,1,1,1), 1:(1,0,0,0))"`, curves (`curve(0:1, 0.5:2 cubic, 1:0)`, one per channel with
  `curve([0:1, 1:2], [0:1])`) and arrays (`array((1,0,0,1), (0,0,1,1))`), sampled exactly as the editor samples them.
- `create niagara-system` from a lightweight template completes it as the editor does when it opens it (newer modules
  and settings), so the engine finds nothing to change.
- Particle effect stacks: `show` lists each emitter's stages and modules in order (disabled ones marked), with inputs
  linked to parameters and dynamic inputs; `niagara NS_Burst module OmnidirectionalBurst add ParticleUpdate
  /Niagara/Modules/Update/Forces/WindForce` adds a module as the stack's + menu does (placed by its dependencies),
  `module OmnidirectionalBurst.Drag disable|enable|delete` changes one, and `set` gives a new module's inputs values.
- Module inputs linked to parameters (`niagara NS_Burst link OmnidirectionalBurst.GravityForce.Gravity
  Engine.Owner.Velocity`) and set to dynamic inputs (`niagara NS_Burst dynamic OmnidirectionalBurst.InitializeParticle.Color
  /Niagara/DynamicInputs/UniformRange/V3/RandomRangeLinearColor`, its own inputs then set as
  `OmnidirectionalBurst.RandomRangeLinearColor.Minimum`), as the stack sets them.
- Particle effect user parameters: `niagara NS_Burst user add Speed float 250` adds one as the system editor's
  parameter panel does (also int, bool, vector, vector2, vector4, color, position, quat, and arrays for baked
  per-particle data: `user add Positions array-float3 "[(0,0,0),(10,0,0)]"`, array-float, array-color, array-int...),
  `user set Speed 300` changes its value, and `show` lists them. Linking an input to a `User.` parameter the system
  does not have adds it with the input's value, and dynamic inputs' own inputs link too (an array user parameter
  feeding Select Linear Color From Array). A set input wins over a value left behind in `show`.
- Particle effect renderers: `show` lists each emitter's renderers with what is set on them;
  `niagara NS_Burst renderer OmnidirectionalBurst add ribbon` adds one as the Render group's menu does (sprite,
  ribbon, light, component, volume), `renderer OmnidirectionalBurst.sprite set Material /Game/M_Spark.M_Spark` (or
  Alignment, SortMode, SubImageSize... and bindings: `set SpriteRotationBinding Particles.Age`) changes one as its
  details do, and `enable|disable|delete` as its stack item does.
- Data interfaces held by module inputs: `niagara NS_Burst data OmnidirectionalBurst.FloatFromCurve001.FloatCurve Curve
  "curve(0:1, 1:0)"` sets a curve (or any property of the data interface) and the compiled copy the effect runs with,
  so nothing needs compiling.
- Empty particle effects: `create niagara-system NS_Spark.uasset` without a template makes one as the Niagara System
  factory does (System State in System Update, its own ids).
- Scratch pad modules: `niagara NS_Burst scratch new ParticleUpdate` makes one as the Scratch Pad's New does (a copy
  of the engine's default module in the system), and `niagara NS_Burst module OmnidirectionalBurst add ParticleUpdate
  ScratchModule` puts it in a stage; `show` lists them.
- Emitters added to a system: `niagara NS_Spark emitter add /Niagara/DefaultAssets/Templates/Emitters/Fountain` adds one
  as the system editor's Add Emitter does (a second one is Fountain001), so a system can be built from empty.
- Module inputs reset: `niagara NS_Burst reset OmnidirectionalBurst.GravityForce.Gravity` puts an input back to its
  module's default as the stack's reset arrow does (a link or dynamic input removed, the default value set).
- Set Parameters modules: `niagara NS_Spark module Sparks set-parameters ParticleUpdate Particles.Position
  Particles.Color` adds a "Set new or existing parameter directly" module last in the stage, as the stack's menu and
  its + menu make it (its own generated script; other parameters as `Particles.Heat:float`). Its inputs are set like
  any module's: values, links, dynamic inputs. With the array dynamic inputs (SelectPositionFromArray...) linked to
  user arrays, user parameters drive every particle's position, colour and size, frame by frame.
- Fixed: emitters added to a system (`emitter add`) made the whole system stop as soon as it started: the system
  graph's emitter nodes named their handles with the id's bytes reordered. Module versions and cached graph ids copied
  by `module add` are exact now too.
- Fixed: engine scripts saved by Unreal 5.4 (among them the SelectPositionFromArray dynamic input) are read whole.
- Errors for unknown module inputs list the module's inputs.
- Material layout: `layout M_Rock.uasset` lays out a material or material function for people to read: each comment
  box's nodes (and each group of nodes outside boxes) in columns flowing left to right, the boxes side by side by what
  feeds what (named reroutes count), never overlapping, the result node at the far right where it was; `layout
  --check` reports overlaps, wires running right to left, nodes off the grid and nodes feeding nothing.
- Behavior tree layout: `layout BT_Guard.uasset` arranges a behavior tree as the editor's Auto Arrange does (each
  node's children side by side below it, centred over their own subtrees, ROOT on top), with node sizes estimated as
  the editor draws them, decorators and services included. The order children run in never changes. Unlike the
  editor, a Simple Parallel's background branch is arranged too, next to its main task. `layout --check` reports
  overlapping nodes and nodes not wired below ROOT.
- Animation blueprint layout: `layout ABP_Hero.uasset` now lays out the animation graphs too. The AnimGraph, layers
  and each state's graph flow left to right into their output pose, saved poses left of where they are used; transition
  and conduit rules flow into their result. State machines read in the order of flow: the entry, then each state a
  column right of the one leading to it (aliases right after the states they stand for), states nothing reaches in a row
  below. Node sizes come from the editor's own (every animation node kind measured). `layout --check` reports
  overlaps, wires running right to left, nodes feeding nothing and states the entry never reaches.
- Material layout: groups of nodes now sit right next to what they feed instead of the farthest edge of their column,
  and nodes that feed nothing stand left of the result node.
- State tree parameters: `state-tree ST_Guard parameter add Speed Float 300` adds one as the tree's Parameters panel
  does (also Bool, Int32, Int64, Double, Byte, Name, String, Text, a struct such as Vector, an object such as Actor, or
  `Class:Actor`, `SoftObject:StaticMesh`...), `parameter set Speed 450` changes its value and `parameter remove Speed`
  deletes it; `show` lists them. Node inputs bind to them: `state-tree ST_Guard Wait bind Tasks[0].Duration
  Parameters.Speed`.
- State trees, utility and linked states: `state-tree ST_Guard Attack consideration Constant` scores a state (the
  parent picks by score with `Root set SelectionBehavior TrySelectChildrenWithHighestUtility`); `Attack type Subtree`
  changes a state's type as its Details panel does; `Use link Attack` runs a subtree from another state and
  `Run link-asset ST_Other` runs another state tree; `Attack parameter add Damage Float 10` gives a subtree its own
  parameters, and on a linked state `parameter set Damage 25` overrides one (`parameter remove` clears the override).
  The linked states follow their subtree's parameters, as the editor keeps them.
- Smart object behaviors: `set SO_Bench DefaultBehaviorDefinitions[0] new:GameplayBehaviorSmartObjectBehaviorDefinition`
  (and a slot's own, `Slots[0].BehaviorDefinitions[0] new:...`: `new:` now works anywhere inside an object), slot data
  such as entrance annotations, and preconditions (`array SO_Bench Slots[0].SelectionPreconditions.EditableConditions
  insert "(Condition=...)"`), which are now prepared for the game as the editor prepares them.
- Widget viewmodels (MVVM, the ModelViewViewModel plugin): `widget W_Health viewmodel add VM_Health` gives a widget
  blueprint a viewmodel as its Viewmodels panel does, and `widget W_Health viewmodel bind VM_Health.Health Bar.Percent`
  binds a viewmodel field to a widget property (`--mode TwoWay` and the others too); `show` lists them. Viewmodel
  variables are marked with `variable VM_Health Health field-notify true`.
- Game Feature actions: `set GFD_MyFeature Actions[0] new:GameFeatureAction_AddComponents`, then fill its
  ComponentList (actor class, component class, client and server); the data's asset bundles are kept up to date as the
  editor keeps them, and `show` lists the actions ("Character -> AudioComponent (server)").
- Fixed: a package whose soft references included an empty one (a class picker left at None next to a set one) could
  not be saved.
- State tree bindings from a state's own parameters (`bind Tasks[0].Duration Attack.Parameters.Damage`) and from
  earlier tasks, global tasks and evaluators (`bind Tasks[1].Duration Tasks[0].Duration`); `show` names every source
  by its state and node.
- Landscapes: `landscape L_World.umap add` makes a landscape as the Landscape mode's New Landscape panel does (8x8
  components of 63 quads by default; `--components 4 4 --sections 2 --quads 31`, `--at`, `--scale`), flat or from a
  heightmap (`--heightmap terrain.png`, a 16-bit grey PNG, or raw `.r16`): its heights, normals, collision and bounds
  computed exactly as the editor computes them. `render` now waits for landscapes to appear. In a World Partition
  level the landscape is split into streaming proxies of 2x2 components (`--grid` to change it), each in its own
  file with its descriptor, as the editor splits it. Any size the New Landscape panel allows (several heightmaps
  beyond 512 vertices).
- New heights for an existing landscape: `landscape L_World.umap heights --heightmap terrain.png` (`--landscape
  <Label>` when there are several), as the Landscape mode's Import writes them: the edit layer, the final heightmaps,
  bounds, collision and, in World Partition levels, every proxy's file and descriptor.
- New heights for part of a landscape: `landscape L_World.umap heights --heightmap hill.png --at 120 40` (a grey PNG,
  its size the region's), as the Landscape mode's Import into a region writes them: only the components it touches
  (and those sharing their heightmaps) are rendered again, as the editor renders them.
- Sculpting landscapes: `landscape L_World.umap sculpt raise --at 120 40 --at 124 42` (also `lower`, `smooth`,
  `flatten`; `--radius`, `--falloff`, `--brush smooth|linear|spherical|tip`, `--strength`, `--mode`, `--kernel`, with the
  Landscape mode's defaults) applies the Landscape mode's sculpting tools with a circle brush at each position, and
  `landscape L_World.umap ramp --from 10 10 0 --to 80 40 500 --width 1500` lays a ramp as the Ramp tool does. The
  heights match the editor's exactly, written as the editor's merge writes them. `sculpt noise`, `sculpt erosion` and
  `sculpt hydro-erosion` run the Noise, Erosion and Hydro Erosion tools (the last without its detail smoothing).
- Landscape splines: `landscape L_World.umap spline --at 10 10 0 --at 30 25 200 --at 50 20 100 --width 300` makes a
  spline as the spline tool's Ctrl+clicks do (each point joined to the one before, rotated to face its neighbours, the
  segments' curves and points, the editor mesh pieces that show them), in levels without World Partition.
  `landscape L_World.umap splines-layer` adds a Splines edit layer, which shapes the ground under the splines as the
  editor does (the road's width flat, its falloffs blending into the terrain); splines added later are applied to it
  at once. In World Partition levels each spline is a spline actor in its own file, as the spline tool makes it there.
- Packed level actors: `create packed-level BPP_Village.uasset --level L_Village.umap` packs a level (without World
  Partition) into a packed level actor blueprint, as the editor's Create Packed Level Actor does: one instanced static
  mesh component per mesh and material combination (hierarchical, with the editor's cluster tree, when it has several
  instances), the same components, instances and bounds the editor saves. Running it again on an existing blueprint
  packs it again after its level changed, as Update Packed Blueprint does (the blueprint keeps its ids).
  `level L_Town.umap add /Game/Props/BPP_L_Village.BPP_L_Village_C` places one, in levels with or without World
  Partition (its actor file and descriptor as the editor saves them).
- World Partition setup: `level L_World.umap world-partition` shows Enable Streaming and the runtime partitions (cell
  size, loading range and the rest, with their HLOD partitions); `world-partition partition MainPartition cell-size
  51200 loading-range 102400`, `world-partition partition add Large cell-size 102400` and `world-partition streaming
  off` change them as World Settings does, and `level <map> <Actor> runtime-grid Large` or `spatially-loaded off`
  set an actor's grid and loading (its descriptor follows).
- HLOD layers: `hlod-layer HLOD_Trees.uasset type merged parent HLOD_Far` sets an HLOD layer's type (instancing,
  merged, simplified, approximated, with the builder settings the editor gives each) and parent layer (make one with
  `create asset HLOD_Trees.uasset --parent HLODLayer`); `level <map> <Actor> hlod-layer HLOD_Trees` puts an actor
  in it, `world-partition partition MainPartition hlod add HLOD_Trees` gives a partition an HLOD partition holding it
  and `world-partition default-hlod-layer HLOD_Trees` makes it the level's default, as World Settings does.
- Private data layers and the data layer hierarchy: `level <map> data-layer add-private Debug` makes a private data
  layer (an editor layer that belongs to the level alone, named as the editor names it), `data-layer DL_Region parent
  DL_World` puts a layer under another (with the engine's rules: a runtime layer takes only runtime children),
  `data-layer Debug rename Tools` renames a private layer, and `delete` gives a deleted layer's children its parent.
  The listing shows the hierarchy, and actors go into private layers like any other.
- External data layers: `level <map> data-layer add EDL_Props` gives a level an external data layer (an
  ExternalDataLayerAsset of a Game Feature plugin, injected while the plugin is active), saved in the plugin as the
  editor saves it, and `level <map> Rock data-layer add EDL_Props` moves an actor into it (its file goes into the
  plugin; `remove` brings it back). The listing shows external data layers with their actors.
- Building HLODs and texture streaming data: `uasset build-hlods <map>` runs the engine's World Partition HLOD builder
  (as Build > Build HLODs does) on a copy and brings the HLOD actors it makes into the level (`--delete` removes them);
  `uasset build-texture-streaming <map>` runs Build Texture Streaming on a copy and saves the map with the data.
  `validate` now also loads a World Partition level's HLOD actors and outliner folders.
- Lighting setups: `level <map> environment` gives a level a sky light, a sun, a sky atmosphere, volumetric clouds and
  height fog as the editor's Environment Light Mixer makes them (or name the parts: `environment sun fog`;
  `second-sun` adds the second atmosphere sun). Works in World Partition levels too.
- Editing level instances in place: `level L_Town.umap LevelInstance_0 edit add PointLight --at 1200 300 200` (or
  `edit <Actor> move|rotate|scale|delete ...`, any level command) edits the instance's level where the instance shows
  it, as the Level Instance edit mode commits it: coordinates are given in the map and saved in the level's own.
  Packed level actors edit their blueprint's level (pack it again to see the change). `level L_Town.umap
  LevelInstance_0 break` moves the instance's actors into the map where they stood and deletes the instance, as
  Break does.
- Landscape materials and paint layers: `landscape L_World.umap material M_Terrain` gives a landscape its material
  (with the material instances each component draws with, as the Details panel makes them), `landscape L_World.umap
  layer add --from-material` (or `layer add Grass Rock`, `--blend none` for layers that are not weight-blended,
  `--info` for an existing layer info) adds the target layers with their layer info assets, as the Target Layers
  panel's "+" makes them, and `landscape L_World.umap layers` lists them. Landscape material nodes (Landscape Layer
  Blend's layers) are saved with every field, as the material editor saves them.
- Painting landscapes: `landscape L_World.umap paint Grass --fill` (the Target Layers panel's Fill Layer), `paint Rock
  --weights rock.png` (a grey PNG or raw 8-bit weights, as the Import of a layer; `--at <x> <y>` for part of the
  landscape) and `paint Puddle --region <x> <y> <w> <h> --weight 200` write the paint layers' weights as the
  Landscape mode does with edit layers: the weightmaps packed into shared texture channels, the final weightmaps as
  the editor's GPU merge renders them (weight-blended layers made to add up to one, every mip), the collision's
  dominant layers and the material instances for each component's layers. Levels with and without World Partition.
- Landscape grass: grass types (`create asset GT_Meadow.uasset --parent LandscapeGrassType`, then `array GT_Meadow.uasset
  GrassVarieties insert "(GrassMesh=/Game/Meshes/SM_Grass.SM_Grass,GrassDensity=25)"`) and a material's Landscape
  Grass Output (`array <m> LandscapeGrassOutput_0:GrassTypes insert "(Name=Meadow,GrassType=...)"`, wired with
  `material-link <m> LandscapeLayerSample_0 "LandscapeGrassOutput_0.Meadow"`), saved as the editor saves them; the
  landscape's components list the material's grass types when it gets the material. Per-platform values
  (GrassDensity, cull distances, LOD screen sizes) can now be created and set (`25` or `(Default=25)`).
- `validate` on a World Partition map also loads every actor of the level (each in its own file) and checks each
  file's resave, and `render` shows a World Partition level's actors.
- See particle effects: `render NS_Burst.uasset --fx-time 0.4` draws a Niagara system 0.4 seconds in, and rendering a
  level now runs its effects for a second first, so they show in the picture.
- Fixed: two engine jobs at the same time (`foliage`, `build-lighting`, `build-navigation`, `render`, `pcg <map>`, from
  two agents or terminals) shared one scratch project and could fail or mix their files; the second now waits.
- Fixed: values filled in from the engine's defaults kept only six decimals (1/60 became 0.016667), so new structs
  differed slightly from the editor's; they are now exact. References written as `Class'/Path'` are accepted
  everywhere a reference is.
- Smart objects on actors: `add-component BP_Bench SmartObjectComponent SmartObject`, then
  `component BP_Bench SmartObject set DefinitionRef.SmartObjectDefinition /Game/AI/SO_Bench.SO_Bench`.
- `set` refuses deprecated properties (such as a smart object component's DefinitionAsset): the engine moves them to
  their replacement when loading, so a value set there was silently lost.
- Common UI input action tables: `create data-table DT_Actions --parent CommonInputActionDataBase`, then
  `table DT_Actions add Confirm DisplayName=Confirm` and `table DT_Actions Confirm set KeyboardInputTypeInfo.Key Enter`
  (a field inside a struct member; keys by name). Rows of structs holding brushes (2D boxes and vectors, Box2f,
  Vector2f) can now be made; before, adding such a row failed.
- New widgets follow the project's "automatic widget variable creation" setting (UserInterfaceSettings): with it off,
  as in Epic's templates, a widget placed in a layout is not a variable (graphs cannot get it); the engine's default
  (on) leaves it one. Before, the tool always behaved as if it were off.
- Fixed: two `validate` runs at the same time (two agents, or two terminals) used the same scratch project and could
  fail with a missing file; the second now waits for the first.
- Fixed: `props` and `show` crashed (stack overflow) on dates and time spans, such as a level sequence's creation
  date; they are now written as Unreal writes them (2026.10.13-06.12.19).
- Level sequences made with `create asset --parent LevelSequence` get new signatures and record the current user and
  time, as the editor's factory does.
- Overriding parent functions that return something: `add-function <bp> ProvideSingleActor --override` makes the
  function graph the editor's Override menu makes (EQS blueprint contexts, BlueprintNativeEvents with outputs...).
- AI perception: `component <bp> AIPerception set SensesConfig[0] new:AISenseConfig_Sight` adds a sense, then
  `set <bp> AISenseConfig_Sight_0:SightRadius 2000`; objects made inside component templates are now saved with the
  editor's load flags.
- Environment queries (EQS): `eqs <EQ> add SimpleGrid`, `eqs <EQ> Option_0 test Distance`, `eqs <EQ> Test_0 set
  TestPurpose Filter`, `move` and `delete`, as the query editor makes them; `show` lists a query's options in the order
  they run, with their generators and tests.
- Arrays of instanced objects: `set <file> GEComponents[1] new:<Class>` adds an entry holding a new object of the class
  (the array's + and class picker), or replaces an entry's object; then `set <file> <Object>_0:<Property> <value>`.
  Gameplay effect components (Chance To Apply, Block Abilities with Tags...) are added this way.
- Gameplay effects: `create blueprint --parent GameplayEffect` makes one as the editor does (with its data version),
  and `set <GE> DurationPolicy HasDuration`, `DurationMagnitude.ScalableFloatMagnitude.Value 2.5`, `Period.Value 1`...
  set its class defaults.
- Gameplay task nodes: `add-node <bp> EventGraph AITask_MoveTo.AIMoveTo` places "Move To Location or Actor", and in a
  Gameplay Ability blueprint ability tasks such as `AbilityTask_PlayMontageAndWait.CreatePlayMontageAndWaitProxy` and
  `AbilityTask_WaitDelay.WaitDelay`, as the editor places them.
- `create blueprint --parent GameplayAbility` (and other parents without a built-in template) adds the greyed-out
  default events the editor adds (Activate Ability, On End Ability...).
- `validate` and the other engine jobs enable the engine plugins the project enables (Gameplay Abilities...), so assets
  whose classes come from them load.
- Submixes: setting a submix's `ParentSubmix` lists it among the parent's `ChildSubmixes` (both files saved), and
  setting `ChildSubmixes` moves the new child, as the Details panel does; effect presets and chains are set as usual.
- Level streaming: `level <map> sublevel <name> transform <x> <y> <z> [<pitch> <yaw> <roll>]` sets a sublevel's
  Level Transform, and `sublevel <name> volumes <Volume>...` the Level Streaming Volumes that load it; `show` lists both.
- Splines: `component <bp> <Spline> points set 0,0,0 500,0,0 500,500,100:Linear` sets a Spline component's points
  (also `add`, `insert`, `remove`, `move`, `type`; without arguments it lists them), with the tangents and distance
  table the editor computes; closed loops too.
- Instanced meshes: `component <bp> <Component> instances add <x,y,z> [<pitch,yaw,roll>] [<scale>]` adds an instance
  to an Instanced Static Mesh component (also `set`, `remove`, `clear`), stored as the editor stores it; `show` lists
  each component's instances.
- Subtitles: `set <SoundWave> Subtitles "[(Text=\"Hello\",Time=0),(Text=\"World\",Time=0.5)]"` sets a sound wave's
  subtitle cues as the Details panel does.
- Fixed: every package in Epic's UE 5.8 project templates (5,042 files) now reads and writes back byte for byte.
  Materials saved by older engines lost the flag of inputs set to a constant, and UE 5.0-5.2 packages got a wrong
  size for their last object. `uasset validate` also checks the remaining files when one fails to load.
- Dialogue: `create asset --parent DialogueVoice|DialogueWave`, then `set` the voice's Gender and the wave's SpokenText,
  VoiceActorDirection and ContextMappings[0].Context.Speaker / .Targets / .SoundWave, as the Details panel does.
- Fixed: setting an object reference by its package path (/Game/Folder/Asset) in a package that already imported that
  package (for another field) pointed at the package itself instead of its asset.
- New objects for instanced properties: `set <asset> <Object>:<Property> new:<Class>` makes an object of the class
  inside the owner, as picking the class in the Details panel does (replacing the one there). For example a camera
  shake: `create blueprint CS_Hit.uasset --parent CameraShakeBase`, then `set CS_Hit.uasset
  Default__CS_Hit_C:RootShakePattern new:PerlinNoiseCameraShakePattern` and `set CS_Hit.uasset
  PerlinNoiseCameraShakePattern_0:Duration 0.5`.
- Package your game: `uasset package [<project>] [--config Development|DebugGame|Shipping] [--out <folder>]` cooks,
  stages and packages the project for Windows with the engine's AutomationTool, as Platforms > Package Project does,
  and lists the errors (a Blueprint-only project takes about a minute).
- Run your tests: `uasset test [<project>] [<filter>]` runs the project's automation tests (functional tests and
  Blueprint tests, under Project by default) headless in its own engine and lists each result with its errors.
- Play your level: `uasset play <map.umap> [--seconds <n>] [--windowed]` runs the level as the game in the project's
  own engine (headless by default) and reports what its blueprints printed (Print String) and the runtime errors and
  warnings, so blueprint logic can be checked without opening the editor.
- Fixed: wiring a new blueprint's grey BeginPlay, Tick or overlap event now makes it a real node, as the editor does;
  before, the event stayed disabled and what was wired to it never ran.
- See your level or asset: `uasset render <map.umap | mesh | material | texture> [--at x y z] [--look-at x y z | --rotation p y r] [--camera <Actor>]
  [--size WxH] [--out file.png]` renders a picture of the level in the installed engine (headless, on copies), from a
  camera that frames the whole level unless one is given; a static or skeletal mesh or a material (on a sphere) is
  shown in a lit preview scene; a texture's source image is written as a PNG directly (no engine needed).
- Project health (free): `uasset health [<project or folder>]` lists packages that assets use but that are missing,
  redirectors left by renames, assets nothing references (levels and assets named in Config left out) and the largest
  assets, from the files alone.
- Compile everything: `uasset compile-all [<folder>]` compiles every blueprint of the project (or of a folder of it) in
  one headless run of the project's own engine, saving nothing, and lists the ones with errors or warnings and what
  the compiler said.
- Level instances: `uasset level <map> add LevelInstance --at <x> <y> <z>`, then `set <map> LevelInstance_0:WorldAsset
  /Game/Maps/L_House.L_House`, places a level inside another as the editor does.
- Sound classes, mixes, attenuation and concurrency: `set <class> ParentClass /Game/Audio/SC_Master` also lists the class
  among the parent's ChildClasses, and setting a parent's ChildClasses moves the children (their parent, and their old
  parent's list), saving each asset involved as the Details panel changes them. `array <asset> <Array> insert` now
  writes every field of a struct entry, as the engine saves them (SoundClassEffects of a sound mix...).
- Sound Cues (Pro): `uasset sound-cue <cue> add <NodeClass> [<x> <y>] | link <Node> <Node|Output> [<input>] |
  unlink <Node|Output> [<input>] | <Node> delete | move <x> <y> | input add | input <n> delete` builds a cue's graph as the Sound Cue editor does
  (Wave Player, Random, Mixer, Modulator, Looping, Attenuation, Delay, Concatenator, Switch... all 22 nodes), and `set
  <cue> WavePlayer_0:SoundWaveAssetPtr /Game/Audio/S_Hit` sets a node's settings; the cue's duration follows. show prints
  the cue's graph. Setting a soft reference (a sound, a level...) now always records it in the package's soft
  reference lists.
- Sublevels: `uasset level <map> sublevel add <other map> [always|blueprint]` and `sublevel <map> delete` add and remove
  sublevels of a persistent level as the Levels window does; show lists them. Validating a level now copies its
  sublevels too, so the engine keeps them.
- World settings: `set <map> WorldSettings:DefaultGameMode /Game/.../BP_MyGameMode_C` (and KillZ, bGlobalGravitySet,
  GlobalGravityZ, LightmassSettings.NumIndirectLightingBounces...) match the editor's Details panel. `set` now reports
  an unsaved property's real default as its value before (KillZ: -1048575, not 0).
- Build lighting: `uasset build-lighting <map.umap> [--quality preview|medium|high|production]
  [--no-reflection-captures]` bakes a level's static lighting with Lightmass and rebuilds its reflection captures, in
  the installed Unreal Engine running headless on copies; the map and its _BuiltData come back into the project (the
  old ones backed up). Projects that don't allow static lighting get their reflection captures only.
- Lights and post process: `set <map> PointLight_0.LightComponent0:IntensityUnits Lumens` (Candelas, EV, Nits,
  Unitless) converts the intensity so the light stays as bright, as the details panel does, for point, spot and rect
  lights; `set <map> PostProcessVolume_0:Settings.BloomIntensity 2` also ticks that setting's override, without which
  it has no effect.
- Runtime virtual textures: `create asset --parent RuntimeVirtualTexture`, `set` its MaterialType, TileCount, bAdaptive
  (the size is clamped as the editor clamps it); a Runtime Virtual Texture Sample node takes the texture's settings when
  its VirtualTexture is set; `level <map> add RuntimeVirtualTextureVolume`, then `set <map>
  RuntimeVirtualTextureVolume_0.VirtualTextureComponent:VirtualTexture /Game/.../RVT_X`. More actors can be placed:
  LocalFogVolume, PainCausingVolume, CameraBlockingVolume, LevelStreamingVolume, the precomputed visibility, lightmass and
  volumetric lightmap volumes, HierarchicalLODVolume, HeterogeneousVolume, LightmassPortal, WindDirectionalSource,
  DefaultPawn, Emitter, DocumentationActor, SplineMeshActor.
- Materials: setting a texture on a sample node now picks its sampler type (normal map, masks, grayscale...) and every
  material or node change keeps the material's list of textures up to date, as the editor does. A property set back to
  its default value is no longer written to the file.
- Subsurface and specular profiles: `create asset --parent SubsurfaceProfile|SpecularProfile`, then
  `set <profile> Settings.SurfaceAlbedo|Settings.MeanFreePathDistance|Settings.Format ...`; a material uses one with
  `set <m> ShadingModel MSM_SubsurfaceProfile` and `set <m> SubsurfaceProfile /Game/.../SP_Skin`. Checked against the
  editor's own.
- Decal, post process, light function and UI materials: set the material's domain (`set <m> MaterialDomain
  MD_DeferredDecal|MD_PostProcess|MD_LightFunction|MD_UI`) and its settings (`BlendableLocation`, `BlendablePriority`,
  `BlendMode`), then wire nodes such as SceneTexture (`SceneTexture_0.Color`) as the material editor does. Every material
  node's output pins now come from the editor's own list, so any named output wires by name.
- Material parameter collections: `uasset mpc <collection> list | add scalar|vector [<Name>] [<default>] | <Name> delete |
  name <New> | default <value>` edits a collection's parameters as its Details panel does (names made unique: Scalar,
  Scalar1...; the collection's state renewed when its size changes). Make one with `create asset --parent
  MaterialParameterCollection`; a material's Collection Parameter node picks up the parameter's ID when its Collection
  and ParameterName are set.
- Material settings and Custom nodes: `set <material> BlendMode|ShadingModel|MaterialDomain|TwoSided|bUsedWith...` now
  updates what the Details panel updates (the shading model field, the material's state); Custom (HLSL) nodes get their
  outputs rebuilt from AdditionalOutputs and their inputs and outputs wire by name. Wiring into a material input that
  was never set now keeps that input's default constant (Roughness 0.5, Base Color black...), as the editor does.
- Material nodes: every one of the engine's placeable material expressions (345 kinds) is added as the editor adds it:
  parameters get a unique name (Param, Param_1...) and their ID, component masks start with R and G, a color ramp gets
  its curve, a named reroute its color, a position transform starts in world space.
- Control Rig hierarchies: `uasset controlrig <rig> parent <Control> <Parent>|none` now moves controls too: the offset
  keeps its place, the control's values stay, and its preferred rotation angles are set as the editor sets them.
- Control Rig graphs: `show` lists a Control Rig's rig graph (its units with their titles, positions and input
  values, the links between them) and its variables, for rigs made in UE 5.8's Content Browser (which are no longer
  blueprints) and for Control Rig blueprints. The rig's compiled form is not needed: the engine rebuilds it from the
  graph whenever it loads the rig.
- Control Rig graphs (Pro): `uasset controlrig <rig> graph add|set|link|unlink|delete` builds a rig's logic without the
  editor: unit nodes from the engine (Forward Solve, Get and Set Transform, Basic IK, math...) with their pins as the
  Control Rig editor makes them, pin values, links and node removal; `variable add|delete` and `graph add get|set`
  add rig variables and their nodes. `create control-rig` now makes the kind of Control Rig UE 5.8 makes (a Control
  Rig asset; `--blueprint` for a Control Rig blueprint), and the hierarchy commands work on both kinds.
- Control Rig hierarchies (Pro): `refresh` brings in the mesh's curves and sockets too (sockets as nulls under their
  bones, tagged MeshSocket), as the hierarchy panel's Refresh does; `uasset controlrig <rig> control <Control>
  type|shape|min|max` changes a control's type (with the limits and value its details panel gives each type), shape,
  color, visibility and limits; `channel add <Control>` adds an animation channel. `show` lists them.
- FBX import (Pro): `uasset import <file.fbx> <new file.uasset>` imports static meshes, skeletal meshes (with their
  skeleton, physics asset and morph targets) and animations (`--animation --skeleton <Skeleton>`) exactly as the
  editor's FBX import does, by running the import in your own Unreal Editor, headless, on a copy: the editor reads
  FBX files with Autodesk's FBX SDK, which cannot be reproduced outside it. `--static`, `--skeleton`,
  `--no-animations` and `--no-materials` work as for glTF files.
- FBX files with several meshes become one asset per mesh as the editor makes them (`--combine`: one), and `uasset
  reimport` updates FBX-made meshes and animations from their source file as the editor's Reimport does. Imported
  assets record the original FBX (not a temporary copy), so the editor can reimport them too.
- IK Rig solvers: `uasset ikrig <rig> solver <n> start|end <Bone>` and `goal|disconnect <Goal>` now work for limb, pole,
  body mover, set transform and stretch limb solvers too, as the solver stack and goal panels set them.
- Child animation blueprints: `uasset anim-override <child abp> <Node> <Anim|none>` makes one of the parent's sequence or
  blend space players play another asset in the child, as the Asset Override editor does (and compiling records it).
- Mirror data tables: `uasset mirror-table <table> update sync|add|update|stale` brings a table up to date with its
  skeleton as the table editor's Reimport from Skeleton, Add Missing, Update Existing and Disable Stale Entries do.
- IK Retargeter ops: `uasset retargeter <rtg> op add pelvis|fk|ik|root|curves` adds one op, set up from the rigs as the
  op stack panel does, and `op <Op|#n> delete|move <index>|enable|disable|name <New>` removes (with its child ops),
  moves, switches and renames one.
- Branching points: `uasset notify <montage> <Name|#n> branch on|off` sets a montage notify's Montage Tick Type as its
  details do and rebuilds the montage's branching point markers, as the notify panel does.
- Montage segments: `uasset montage <montage> segment <n>:<i> rate|start|end|loops <value>` sets a segment's play rate,
  start and end time and loop count as its details panel does; the segments close up and sections and notifies follow
  as in the editor. Sections and notifies past the end of a montage that got shorter now move to the end, as the
  editor moves them (they were moved in proportion).
- Pose assets: `uasset pose <pose asset> <Pose>[,<Pose>...] delete` and `<Pose> name <New>` delete and rename poses as
  the pose viewer does.
- Control Rig hierarchies: `uasset controlrig <rig> delete <Element>`, `rename <Element> <New>` and `parent <Element>
  <Parent>|none` delete, rename and move bones, nulls and controls as the hierarchy panel does (children and moved
  elements keep their place in the world; moving controls is not supported yet).
- IK Rigs: `uasset ikrig <rig> goal|chain <Name> delete`, `goal|chain <Name> name <New>` and `exclude|include <Bone>`
  remove and rename goals and retarget chains (the chains and solvers using a goal follow it) and exclude bones from the
  solvers, as the IK Rig editor does.
- Animation modifiers: `uasset modifier <anim> add <ModifierClass>` adds a modifier (a blueprint of
  AnimationModifier, made with `uasset create blueprint <file> --parent AnimationModifier`, or a built-in one such as
  ZeroOutRootBoneModifier) to an animation as the Animation Data Modifiers tab adds it, and `<#n> delete` removes one;
  `show` lists them. Applying a modifier runs its blueprint code, which only the editor does: right-click the
  animation, Animation Modifiers, Apply.
- Animation blueprints: `uasset create anim-blueprint <new file> --template` makes a template (no skeleton) and
  `--parent <AnimBlueprint>` a child of another, as the New Animation Blueprint dialog makes them. A skeletal mesh's
  post-process animation blueprint is set with `uasset set <mesh> PostProcessAnimBlueprint <ABP_C>`.
- Montages, composites, pose assets and mirror tables made from another skeleton or animation than the built-in
  starting file now name it in their asset registry tags too, so the editor's skeleton-filtered asset pickers list them
  before they are first resaved.
- Pose assets: `uasset create pose-asset <new file> --animation <Anim> [--names A,B,...]` makes one as Create Pose Asset
  does: a pose per frame of the animation with the bones that differ from the reference pose and the curve values,
  named from the list and then Pose_0, Pose_1...; `show` lists the poses and what each moves.
- Mirror data tables: `uasset create mirror-table <new file> --skeleton <Skeleton>` makes one as the editor's Mirror Data
  Table dialog does: a row per bone, notify, sync marker and curve, paired by the project's find and replace expressions
  (Animation settings), unpaired names mapped to themselves, pairs missing their other half disabled.
- Data tables of engine row structs: rows added or changed with `uasset table` now save every field, as the editor
  does; before, a value equal to the type's zero (bEnabled false, an empty comment) was left out and read back as the
  struct's default.
- Animation composites: `uasset create composite <new file> --animation <Anim>` makes a composite of an animation as
  Create AnimComposite does, and `uasset composite <composite> segment add <Anim> [--at <s>] | segment <i> delete` adds
  and removes animations as the composite editor does (packed end to end, length and frame rate updated, notifies moved
  with the end as the engine moves them). `uasset notify` adds notifies to composites. `show` lists segments and notifies.
- Editing an array of structs that grows no longer changes an earlier entry's object reference when the new entry
  references another asset.
- Blend spaces and aim offsets: `uasset blendspace <bs> sample add|move|delete`, `axis`, `grid on|off` edit them
  as the blend space editor does, saving the same sample triangulation, segments or grid weights. Make them with
  `create asset --parent BlendSpace|BlendSpace1D|AimOffsetBlendSpace|AimOffsetBlendSpace1D --skeleton <Skeleton>`.
  `show` lists axes and samples.
- Animation montages: `uasset create montage <new file> --animation <Anim>` makes a montage of an animation as
  Create AnimMontage does, and `uasset montage <montage> section|slot|segment ...` adds, links and deletes sections,
  adds and deletes slot tracks (registering the slot on the skeleton) and adds and deletes animation segments, as the
  montage editor does. `uasset notify` adds and deletes montage notifies, linked to the segment under them.
  `show` lists sections, slots, segments and notifies.
- Paper2D tile sets and tile maps: `uasset create tileset`, `uasset create tilemap` and `uasset tilemap <map> paint|erase`
  make and paint them as the editor's Create Tile Set, Create Tile Map and paint tool do.
- Paper2D flipbooks: `uasset create flipbook <new file> --sprites <Sprite> ... [--fps n]` makes a sprite animation
  as the editor's Create Flipbook does.
- Paper2D sprites: `uasset create sprite <new file> --texture <Texture>` makes a sprite of a texture as the editor's
  Create Sprite does (tight render and collision boxes, centre pivot, translucent or masked material).
- Reading editor-compressed data: textures' source pixels the editor stored compressed (Oodle) are read with the
  Oodle library of the user's engine, so tools that need a texture's pixels work on editor-imported textures too.
- Font sub-fonts: a font's sub-font families (fonts for other scripts' character ranges) are added with
  `uasset array <font> CompositeFont.SubTypefaces insert ...`, saved as the font editor saves them (see the skill).
- Surround sounds and cue points: `uasset import` takes WAV files with 4, 6 or 8 channels (and ambisonics, named
  _ambix or _fuma) and keeps a WAV's cue points, labels and loop regions, as the editor's sound import does.
- Animated morph targets: a glTF animation's morph target weights are imported as curves of the animation, keyed as
  the file keys them, as the editor imports them; importing only animations adds their morph curves to the skeleton.
- Animation curves: `uasset curve <anim> add <Name> <seconds>=<value> ...` adds a float curve to an animation sequence
  (morph targets of the same name follow it; animation blueprints read it), and `curve <anim> <Name> delete` removes
  one, as the editor's animation data controller does; `show` lists them.
- Translation retargeting: `uasset mesh <skeleton> retarget <Bone> <Mode> [--children]` sets how a bone's animation
  translation is retargeted (Animation, Skeleton, AnimationScaled, AnimationRelative, OrientAndScale), as the skeleton
  tree does; `show` lists the bones not on Animation.
- Audio formats: `uasset import` takes 8-, 24- and 32-bit and float WAV files, AIFF, OGG, FLAC, Opus and MP3, converted
  to 16-bit WAV by the engine's own libsndfile exactly as the editor converts them.
- OBJ materials: `uasset import` of an OBJ file also makes the materials of its .mtl files and the textures they use, as
  the editor does (Phong, unlit, PBR and translucent instances of the Interchange materials; textures named TEX_<file>).
- glTF meshes with several UV sets keep them all (the lightmap uses the last, as in the editor), and sparse accessors
  are read.
- glTF material extensions: clear coat, sheen, transmission, specular, IOR, iridescence, anisotropy, volume, emissive
  strength and specular-glossiness materials import as the editor imports them; a parameter is saved only where the
  parent material has it and its value differs, as the editor does. Grey glTF textures stay in colour, as in the editor.
- OBJ files without texture coordinates import with the box-projected UVs the editor gives them.
- `uasset import <image.hdr> --2d` imports an HDR image as a 2D texture (BC6H compressed) instead of a cube map.
- Photoshop images: `uasset import` takes .psd files (grayscale or RGB, 8 or 16 bits, with or without alpha) and
  imports their flattened image as a texture, as the editor does.
- Video import (Pro): `uasset import` takes video and media files (.mp4, .mov, .avi, .wmv and the other formats the editor's
  media factory takes) and makes a File Media Source that plays it, as the editor does (the path relative to Content
  when the file is there).
- glTF materials and textures (Pro): `uasset import` of a glTF file also makes its materials and the textures they use
  beside the mesh, as the editor's glTF import makes them: material instances of the glTF material (M_GLTF with
  Substrate) with the factors, textures, texture switches, blend mode and two-sidedness; textures from embedded or
  external images with the sampler's wrap and filter, sRGB from their use and normal maps flipped green.
  `--no-materials` skips them; assets already there by name are used as they are.
- `set-param` sets static switch parameters (true/false); an instance whose overrides differ from its parent now gets
  its own shader permutation as the editor gives it. `validate` loads assets with the project's Substrate setting.
- k-DOP collision (Pro): `uasset mesh <file> collision add kdop10x|kdop10y|kdop10z|kdop18|kdop26` fits a convex hull with
  10, 18 or 26 sides as the static mesh editor's Collision menu does (the same vertices); the engine adds its
  triangles when it next loads the mesh.
- Animation import (Pro): a skinned glTF file's animations become animation sequences beside the skeletal mesh
  (<Name>_Anim, or one per animation), baked frame by frame exactly as the editor's import bakes them, with the same
  keys and data guid; `--no-animations` skips them. `uasset import <anim.glb> <file> --animation --skeleton <Skeleton>`
  imports only the animations onto an existing skeleton. `show` lists an animation's skeleton, length, frame rate
  and animated bones.
- Skeletal mesh import (Pro): `uasset import` makes a skeletal mesh and its skeleton (<Name>_Skeleton) from a glTF
  file with a skinned mesh, with the geometry, skin weights, tangents and bone poses exactly as the editor's glTF
  import reads them; the engine builds the render data when it first loads the mesh. `--skeleton <Skeleton>` makes it use an
  existing skeleton that has its bones, so characters share animations; `--static` imports the mesh as a static mesh
  instead. `show` lists a skeletal mesh's skeleton, material slots and bone tree, and a skeleton's
  bones; `set-material` changes a skeletal mesh's slots (UE 5.8 keeps them outside the properties).
- Skeletal mesh packages saved by UE 5.8 now open and save byte for byte (a skin weight setting of an optional type
  lost 12 bytes).
- HDR import (Pro): `uasset import` also takes Radiance .hdr images and makes a cube map from them, as the editor does
  (the long-lat image kept as RGBE, HDR compression), for skies and reflection captures.
- BMP import (Pro): `uasset import` also takes Windows bitmaps (8-bit palette, 16, 24 and 32-bit, with or without
  alpha), decoded as the editor decodes them.
- PNGs with transparent backgrounds (binary transparency: pixels fully visible or fully transparent white) now import:
  the transparent pixels take the colour of the visible ones nearby, as the editor fills them, so edges do not show a
  white fringe. They were refused before.
- glTF mesh import (Pro): `uasset import` also takes glTF files (.glb, or .gltf with its buffers), the format most 3D
  generators export, and makes a static mesh with the geometry exactly as the editor's glTF import reads it (metres to
  centimetres, Y up to Z up, node transforms baked in, vertex colors, a slot per glTF material).
- Mesh LODs (Pro): `uasset mesh <file> lods <count>` sets how many levels of detail a static mesh has, as the LOD
  settings' Number of LODs does: each new level keeps half the triangles of the one before, generated by the engine.
- Mesh sockets (Pro): `uasset mesh <file> socket add <Name> [--at x y z] [--rotation p y r] [--scale x y z] [--tag t]`
  and `socket <Name> delete` add and remove a static mesh's sockets as the Socket Manager does; the mesh's own copy of
  the socket list now follows every edit.
- Mesh collision (Pro): `uasset mesh <file> collision add box|sphere|capsule` fits a simple collision shape as the
  static mesh editor's Collision menu does (same sizes, byte for byte), `collision clear` removes them, and
  `collision complex|simple` switches the mesh to use its own triangles as collision. Meshes made with `create mesh`
  get collision by default (a box or sphere where exact, otherwise their triangles; `--collision` picks).
- Simple meshes (Pro): `uasset create mesh <file> box 200x100x50 | plane | cylinder | cone | sphere | extrude <height>
  <x,y> ...` makes a static mesh without a source file (centimetres, normals and UVs, hard edges where flat faces meet),
  for blockouts and placeholders; `--material` sets its material.
- OBJ mesh import (Pro): `uasset import` also takes Wavefront OBJ files and makes a static mesh: the geometry exactly as
  the editor's OBJ import reads it (kept inside the mesh as its editable source), a material slot per OBJ material
  (`--material <Slot>=<material>` picks each slot's material; others get the WorldGridMaterial), and the bounds, counts
  and texture-streaming densities the editor computes. OBJ files need texture coordinates.
- Font import (Pro): `uasset import` also takes TrueType and OpenType fonts (.ttf, .otf, .ttc, .otc) and makes a
  font face as the editor's font import does; `--font` also makes the <Name>_Font font that uses it, as the editor
  offers to. Fonts' typefaces now read as fields, so faces can be added or changed with `set`
  (`CompositeFont.DefaultTypeface.Fonts[1] "(Name=Bold,Font=(FontFaceAsset=/Game/UI/F_Bold.F_Bold))"`).
- WAV import (Pro): `uasset import` also takes 16-bit PCM WAV files (mono or stereo) and makes a SoundWave as the
  editor's sound import does: the file kept inside the sound, its channels, sample rate and duration, and the reimport
  record.
- JPEG import (Pro): `uasset import` also takes JPEG files, kept as JPEG inside the texture (as the editor's texture
  import does with RetainJpegFormat), so nothing is lost to recompression.
- TGA import (Pro): `uasset import` also takes TGA files (16, 24 and 32 bits, raw or RLE; 8-bit grey and colour-mapped
  ones become Grayscale, linear textures), as the editor's texture import does.
- Placeholder textures (Pro): `uasset create texture <file> <W>x<H> solid|gradient|checker|noise ...` makes a texture
  without a source file (a colour, a gradient, a checkerboard or grey noise), set up as an import would set it up.
- Texture import (Pro): `uasset import <image.png> <file.uasset>` imports a PNG as a Texture2D exactly as the editor's
  texture import does (any PNG kind; grey images as G8; 16-bit kept; normal maps detected; non-power-of-two settings;
  the source stored so the editor can rebuild and reimport it). `show` summarizes textures.
- Editor utility blueprints and naming tokens (Pro): `create editor-utility|editor-utility-actor|naming-tokens|
  editor-utility-naming-tokens <file>` makes them as their factories do; they are edited like other blueprints.
- Composite data tables (Pro): `create data-table <file> --parent <RowStruct> --composite` makes one as the editor's
  factory does for that row struct (native or a struct asset); its parent tables are set with `set`.
- Animation assets of a skeleton (Pro): `create asset --parent AnimMontage|AnimComposite|BlendSpace|BlendSpace1D|
  AimOffsetBlendSpace|AimOffsetBlendSpace1D --skeleton <Skeleton>` makes them as the editor's factories do for that
  skeleton (its reference, registry tag and GUID, read from the skeleton asset).
- Assets whose factory asks for a class (Pro): `create asset --parent <Class>` makes curves (float, vector, color),
  source and submix effect presets, audio analyzers and their settings, Interchange pipelines, transform provider data
  and geometry collection caches as the editor's factory makes them for that class (60 classes), each loaded by the engine.
- Widget animations (Pro): `widget-anim` adds, renames and deletes a widget blueprint's animations and keys widget
  properties in them (opacity and other numbers, colors, the render transform), as the Animations tab and Sequencer's
  key button do: the widget gets a binding and the property a track the first time, keys are smooth, and the play range
  follows the keys. `show` lists each animation with its keys. Renaming an animated widget keeps it animated.
- World Partition levels (Pro): `show` lists the actors saved in their own packages (one file per actor), and `level`
  and `set` move, turn, scale, label, change, delete and put them in folders; each save rewrites the actor's World Partition
  descriptor as the editor does (its transform, streaming bounds, label and folder), and folders are made as the
  level's folder objects. `level ... add|copy` places new actors in packages of their own, as spawning them does.
- Widget navigation (Pro): `widget ... nav <Direction> <Rule> [<Target>]` sets where focus goes from a widget (Explicit to a
  widget, Wrap, Stop, Custom functions...), as the Navigation details do; `show` lists it. Replacing a widget that has
  navigation drops it as the editor does, and border slots now set their border's padding and alignment.
- Named slots (Pro): `widget ... add <Class> --parent <UserWidget>.<Slot>` fills a named slot of a user widget placed
  in the tree, as dropping a widget onto it in the Hierarchy does; deleting the widget empties the slot, and `show`
  lists slot contents under their user widget. Duplicating a blueprint now forgets its open tabs, as the editor does.
- Widget property bindings (Pro): `widget ... bind <Property> [<Function|Variable>]` binds a widget property to a
  function or variable, or makes a new Get<Widget><Property> function for it, as the Details panel does; `unbind`
  removes one, and `show` lists them. Functions whose output is named ReturnValue now compile it as their return value.
- Widget blueprints (Pro): `widget ... wrap <Panel>` and `widget ... replace <Class>` do the Hierarchy's Wrap With
  and Replace With as the editor does (values, slots and children carried over, names kept or references renamed).
  Duplicating a widget blueprint now renames the category of its widget variables, as the editor's compile does.
- Function nodes checked against the editor's whole Blueprint palette (about 11,800 calls): set and map library
  functions (Map Add, Set Union...) and "any value" parameters now take wildcard pins, and enum pins start at the
  enum's first entry, as the editor makes them.
- Project blueprints in `find` and `describe`: `describe BP_Player` lists a blueprint class's parents,
  interfaces, variables with their defaults, functions with inputs and outputs, custom events, event dispatchers and
  components; `find` searches the project's blueprints (and its plugins') and their members. The index is kept in
  the project's Saved folder and follows file changes.
- Engine defaults: Make Struct pins of engine structs and the expose-on-spawn pins of Construct Object, Spawn Actor
  and Create Widget start at the engine's real default values (a team id of 255, multipliers of 1.0...), with their
  tooltips, as the editor makes them; `describe` shows each property's default and the inherited defaults a class
  changes. The data comes from the UE 5.8 editor and covers the engine and its default plugins.
- Values (Pro): `set` writes every saved property type back from the text `props` shows, whole lists, sets and
  maps included, and also takes the editor's copy text ((a,b), ((key, value),...)). `props` now shows object
  references inside native values as paths, enum values by name, material inputs with what feeds them, and quotes
  names that need it. Every property of the test assets reads back byte for byte.
- C++ plugins (Pro): `create plugin --template` makes plugins from every New Plugin wizard template (Blank,
  Blueprint Library, Editor Toolbar Button, Editor Standalone Window, Editor Mode, Third Party Library, Game Feature
  with C++) as the wizard does, and `build` compiles them, also in Blueprint-only projects.
- C++ projects (Pro): `create project --cpp` makes a template's C++ version as the editor does (its code renamed
  to the project), and `build` compiles a project's code with the engine's UnrealBuildTool, listing the compiler's
  errors.
- Localization (Pro): `localization` sets up a target's cultures and what it gathers, runs the Localization
  Dashboard's gather, export, import and compile headless (the config scripts written as the dashboard writes them),
  and lists and fills in the exported PO files' translations.
- String tables (Pro): `create string-table` and `string-table set|delete|namespace|meta` edit string tables as their
  editor does (the localization gather data kept in step), and texts (`set` on text properties, `set-pin` on text
  pins) take `LOCTABLE("/Game/.../ST_Table.ST_Table", "Key")`. UE 5.8 string tables with notes now read correctly.
  A blueprint variable's value saved for the first time now carries the variable's guid, as the editor saves it.
- Redirectors and folders (Pro): `redirectors` lists the redirectors renames left behind and `redirectors ... fix`
  fixes them up as the editor's Fix Up Redirectors does; `folder create|move|delete` manages Content folders with
  their assets. `move-asset` can now move an asset to another folder without renaming it.
- Settings maps, platforms and objects (Pro): `settings` sets map settings (`add <Key> <Value>`, `remove <Key>`,
  `set`), writes a platform's own config file with `--platform Windows`, and a per-object config section with
  `--object <Name>` (device profiles: `DeviceProfile CVars add r.ViewDistanceScale=0.5 --object Windows`).
- Gameplay tag values (Pro): `set` on tag, tag container and tag query variables and `set-pin` on tag pins take
  plain tags (`Ability.Fire`, `Ability.Fire, Status.Burning`) and queries (`ALL(ANY(A, B), NONE(C))`), checked
  against the project's tags and written as the editor's tag widgets write them (queries built as the query editor
  builds them, the tags listed for the asset registry's reference search). `tags` lists the tags of the project's tag
  tables. `set-pin` now refuses by-reference and container inputs, which the editor wires only.
- Component collision (Pro): `component <file> <Component> collision <Preset>` sets a component's collision as its
  details panel does: the preset's collision, object type and responses are copied in, `Custom` takes its own
  (`--enabled`, `--object`, `--respond Pawn=overlap`), `Default` uses a static mesh's own collision, and only what
  differs from the component's defaults is saved. It works on the blueprint's components, a parent blueprint's and those
  a native parent makes (a character's capsule and mesh). `validate` now loads assets with the project's collision
  channels and presets, physical surfaces and gameplay tags.
- Physical surfaces (Pro): `surfaces <project>` lists the surface types and their names; `add`, `name` and
  `remove` edit them as Project Settings > Physics does (no two types share a name). A physical material's
  SurfaceType can be set by the surface's name.
- Gameplay tags (Pro): `tags <project>` lists the project's tags (explicit and implied, their sources and redirects);
  `tags <project> add|rename|delete` edits them as the tag editor does (tag rules, children renamed with redirects,
  tags still used by assets kept), in DefaultGameplayTags.ini or a Config/Tags source file.
- Collision (Pro): `collision <project>` lists the object and trace channels and presets; `channel add|rename|default|
  delete` and `preset add|respond|collision|object|help|rename|delete` edit them as Project Settings > Collision does
  (first free game channel, responses kept where they differ from the defaults, engine presets changed through
  EditProfiles, renames with redirects).
- List settings (Pro): `settings <project> <Class> <List> add|remove|clear|set` edits arrays and sets with the config
  files' own commands (+, -, !, ^, keyed lists such as PrimaryAssetTypesToScan replacing by key); the engine reads the
  intended lists (checked with obj dump). `settings <project> <Class>` shows lists as the engine's files combine them.
- Project settings: `settings <project> [--find <words>]` lists the settings classes, `settings <project> <Class>`
  their settings and the project's values; `settings <project> <Class> <Setting> <value>` (Pro) sets one as the
  Project Settings window saves it (UpdateSinglePropertyInConfigFile: values exported as the engine exports them,
  console variable keys, only that line of the Default ini rewritten).
- New plugins (Pro): `create plugin <project> <Name> [--game-feature]` makes a content-only plugin or Game Feature
  as the New Plugin wizard does (descriptor, icon, Content folder, the project reference a Game Feature needs, its
  GameFeatureData asset). Assets can now be created inside plugins' Content folders, and `validate --in-project`
  loads plugin assets by their mount point.
- Plugins: `plugins <project> [--all]` lists what a project enables (its references, the plugins enabled by
  default, their dependencies); `plugin <project> enable|disable <Plugin>` (Pro) is the Plugins browser's checkbox,
  saving the project file as the editor does (disabling a plugin disables the enabled plugins that need it).
- New projects (Pro): `create project <folder>/<Name>.uproject [--template <Template>] [--variant <Variant>]`
  makes a blueprint project from any of the engine's templates as the New Project dialog does (template files with
  their renames and replacements, the dialog's config values, shared content packs, the project file);
  `--mobile` and `--scalable` are the dialog's target and quality choices. `templates` lists the templates.
- A material instance given a parent (`create material-instance --parent`, `set <instance> Parent`) now takes the
  parent's base properties (blend mode, shading model, two sided, opacity mask clip value, usage flags...) where it
  does not override them, as the editor does (UMaterialInstance::UpdateOverridableBaseProperties).
- Material instance layer stacks (Pro): `material-layers` on a material instance edits its layers as the
  material instance editor's layer panel does: they follow the parent's until changed (unlink, relink), removing or
  moving a layer takes its parameter overrides along, and saving adds what the editor adds (physical material,
  refraction depth bias, static permutation). `show` lists an instance's own stack.
- Material layer stacks (Pro): `material-layers` lists and edits a Material Attribute Layers node's stack (add a
  layer and its blend, remove, swap, show or hide, rename, change a layer or blend), as the material editor's layer
  panel does (FMaterialLayersFunctions); `show` lists the stack. `material-link` can connect Material Attributes.
- Arrays, sets and maps of natively serialized structs (Guid, Vector...) are now tagged as the engine tags them.
- Material layers and function instances (Pro): `create material-layer`, `material-layer-blend` (with the nodes the
  material editor adds when it first opens them), `material-function-instance`, `material-layer-instance` and
  `material-layer-blend-instance` (`--parent`, as UMaterialFunctionInstance::SetParent: base function and usage);
  `set-param` overrides a function instance's parameters; `show` lists a function instance's parent and overrides.
- Material instance parameter entries now save every field, as the editor does (a scalar's AtlasData was missing),
  and empty soft object references save None, as the engine writes them.
- `bt <file> copy <Node>,... [--from <tree>] [onto <Node>] [at <x> <y>]` (Pro) copies and pastes behavior tree
  nodes as the editor does (FAIGraphEditor::CopySelectedNodes, PasteNodesHere), within a tree or from another one, with
  their decorators, services and composite decorators.
- Composite decorators in behavior trees (Pro): `bt <file> <Node> composite`, then `bt <file> <Composite> add`
  decorators and AND/OR/NOT nodes, `link`, `unlink`, `add-pin`, `delete` and `set`, as the behavior tree editor
  builds them: the tree's DecoratorOps, each decorator's parent, the composite's description (every engine decorator's
  description is reproduced, with the class defaults the editor reports) and its abort flag. `show` draws the logic.
- `add-node <file> <Graph> math "<expression>"` (Pro) adds a Math Expression node built from a formula as the editor
  builds it (FMathGraphGenerator): inputs for unknown names, Get nodes for variables, the function libraries' operators
  and functions, and the conversion nodes the editor inserts between types (int to double...). `title` on the node
  rebuilds it from a new formula, keeping its wires. `show` titles it with its formula; `validate` ignores the node
  renumbering the engine does when it rebuilds the formula's graph on load.
- `add-node <file> <Graph> <Class>.<Function>` (Pro) places async actions (Async Save Game to Slot, Download Image,
  Async Load Primary Asset...) as the editor does: a node with an exec output per event of the action and the event's
  values. `find` lists async action functions too.
- `add-node <map> EventGraph actor-event <Actor> <Dispatcher>` (Pro) adds an event of an actor placed in the level
  (OnActorBeginOverlap of Door...) to its level blueprint, as the editor's "Add Event for Door" does.
- Level blueprints (Pro): `uasset level <map> blueprint` gives a level without one its level blueprint, as the
  editor's Open Level Blueprint makes it (with the disabled BeginPlay and Tick events and the level script actor).
- Material functions (Pro): `create material-function`; `show` lists a function's inputs and outputs in the order
  calls list them; the material node commands edit functions (FunctionInput and FunctionOutput nodes get unique names,
  every edit renews the function's state as the editor does), and `add-material-node <material> <MF_Name>` adds a call
  of a function with its inputs and outputs, wired by name (`MaterialFunctionCall_0.Strength`).
- Blackboards (Pro): `show` lists a blackboard's keys with their types and settings; `uasset blackboard` adds keys
  (named as the editor names them: FloatKey, FloatKey0...), copies, renames, retypes and deletes them, sets their
  description, category, instance sync and type settings (base class, enum, default value), and sets the parent
  blackboard (the SelfActor key follows, as in the editor).
- Behavior trees (Pro): `show` draws a behavior tree from ROOT down with the editor's execution numbers, titles,
  decorators, services and node settings, and lists nodes not connected to the tree; `uasset bt` adds composites and
  tasks (every engine node, by name or title), decorators and services, deletes, moves, wires and unwires nodes,
  sets node settings (a key selector takes a blackboard key the node accepts) and sets the tree's blackboard. After
  each change the runtime tree is rebuilt as the editor rebuilds it, and nodes pick their blackboard keys as the
  editor does.
- Behavior trees take the project's blueprint tasks, decorators and services (BTT_..., BTD_..., BTS_...) by name;
  their Blackboard Key Selector variables pick keys as the editor's do.
- Timelines (Pro): `show` lists a blueprint's timelines with their tracks and keys; `uasset timeline` adds Timeline
  nodes, tracks (float, vector, color, event), keys on them, and settings (length, auto play, loop...), as the
  editor makes them. Deleting a Timeline node removes its timeline.
- Select nodes take a bool or enum index when wired: False/True options, or one option per enum entry, as in the
  editor.
- `uasset search <folder> <text>` (free) finds text in the views of every blueprint, struct, enum and data table under
  a folder, with the graph and node of each match.
- `set-pin` takes object and class references (assets, native classes, blueprints); setting a spawn, construct or
  create-widget node's class rebuilds it for that class. `set-var` sets object, class, struct and container variables.
- `uasset reset` puts a saved value back to its default; `uasset array` inserts, removes and clears array and set
  entries, and `uasset map` puts and removes map entries; empty containers are created when first edited, and a
  blueprint's own variables are found in its class defaults. Struct values may leave fields out (they keep their
  defaults).
- Create assets of any class (Pro): `uasset create asset <file> --parent <Class>` makes input actions, input mapping
  contexts and data assets (of native or blueprint classes); `set` then sets their values, including variables of
  blueprint classes.
- Data tables (Pro): `uasset create data-table <file> --parent <RowStruct>` makes one; `show` lists a table's rows; `uasset table` adds, sets, renames, copies, moves and deletes rows,
  saving only values that differ from the struct's defaults, as the editor does, and imports or exports them as CSV.
- Data tables (and any asset whose import data comes first) now write back byte-identical.
- Structs and enums (Pro): `uasset create struct|enum` makes new ones; `uasset struct` adds, renames, retypes,
  reorders and deletes members and sets their defaults, tooltips and flags, recompiling the struct as the editor does;
  `uasset enum` adds, renames, reorders and deletes entries and sets their tooltips.
- Rename and move assets (Pro): `uasset move-asset <file> <new file>` renames or moves an asset and updates every asset,
  level and config file of the project that uses it (child blueprints, variables, casts, spawn nodes, default game
  mode...), as Rename and Fix Up Redirectors do in the editor.
- `set` creates a blueprint's unsaved class defaults inherited from its native parents (bReplicates, tick settings,
  InitialLifeSpan...), in the order the engine saves them. `show` lists Class Settings (description, category, display
  name, namespace, abstract, const, deprecated...) under `class`; `set <BP>:BlueprintDescription` and the like change them.
- Reparent blueprints (Pro): `uasset class <file> parent <Class>` changes the parent class to a native class or another
  blueprint, as the editor saves it: config and class flags, the parent's built-in components (a character's capsule
  and mesh), and the default scene root giving way to the parent's root.
- Create blueprints (Pro): `uasset create blueprint <file> --parent Actor|Pawn|Character|GameModeBase|...` (15
  parents, and any other Blueprintable class or blueprint through reparenting) and `uasset create
  interface|function-library|macro-library|widget <file>` make the empty blueprints the editor makes. Duplicating a blueprint now also renames the paths in its localization data.
- `link` types wildcard pins as the editor does: reroutes, Make Array and Make Set, Get, Select and array functions
  take the wired type, and math operators switch to the function for it (Add_VectorVector for vectors), so the
  engine keeps the wire. A wired input goes back to its original value, as in the editor.
- Add and remove pins (Pro): `uasset pin <file> <Node> add` and `pin <Node.Pin> remove` for Sequence outputs, Make
  Array and Make Set entries, Select options, Switch cases (and their Default pin), and extra inputs of And, Or, Add
  and other operators; `pin <Node.Case> name` renames string and name switch cases. And, Or, Min, Max and the like
  are now placed as the editor places them, as nodes that take more inputs.
- Split struct pins (Pro): `uasset pin <file> <Node.Pin> split|recombine` splits a struct pin into its members
  (nested structs too) and recombines them, as the editor does; split pins survive node rebuilds.
- Components (Pro): `uasset add-component` adds any component class, nested under a parent or socket, saved as
  the editor saves it; `uasset component` renames, deletes, re-attaches or makes one the root. Component properties
  are set with `uasset set <Name>_GEN_VARIABLE:<Property>`.
- Graphs (Pro): `uasset graph` adds event graph pages and renames or deletes any graph.
- Macros (Pro): `uasset macro` adds a blueprint macro with exec and data pins, changes its pins, renames or deletes
  it; `add-node macro <Name>` places this blueprint's macros too.
- Interfaces (Pro): `uasset interface add|remove` implements an interface on a blueprint (its function graphs and the
  compiled class's interface) or removes it, optionally keeping its functions as ordinary ones.
- Event dispatchers (Pro): `uasset add-dispatcher` adds one with parameters, as the editor makes it; `uasset
  dispatcher` renames, deletes or changes its parameters, rebuilding its Bind, Unbind and Call nodes.
- Function settings (Pro): `uasset function` sets pure, const, access, category, tooltip, keywords, compact title,
  call in editor, deprecation, thread safety; calls of the function are rebuilt as the editor rebuilds them.
- Rename, retype and delete variables (Pro): `uasset variable <file> <Var> name|type|delete`, updating their Get and
  Set nodes here and in the project's other blueprints.
- `add-node get|set BP_Other.Variable` reads and writes another blueprint's variable; inherited blueprint variables
  work by name.
- Switch on an enum with more than five entries hides its advanced pins, as the editor does.
- `variable <Var> replication rep-notify` adds the OnRep function as the editor does. New functions in function
  libraries are static, in const blueprints const, in editor utility blueprints callable in the editor.
- Calls of blueprint functions with array inputs pass them by reference, as the editor does.
- `set` reaches blueprint nodes by the ids `show` prints (EventGraph:Comment_0), so comment boxes, reroutes and
  every node can be resized, recolored and adjusted; `show --all` prints each node's layout settings.
- Edit any asset (Pro): `uasset set` changes any saved property by path (`StaticMaterials[0].MaterialInterface`,
  `RelativeLocation.X`...), creating properties left at their default; `uasset set-material` sets a mesh's
  material slots. Replacing a reference leaves no stale import behind.
- Materials (Pro): `uasset create material|material-instance`, `add-material-node`, `material-link`,
  `material-unlink` and `set-param` build material graphs and instances; `show` prints materials, material
  instances and meshes.
- Assets (Pro): `uasset duplicate` copies any asset, `uasset delete` removes assets nothing uses (into the
  backups; `--skip-used` keeps the used ones and goes on), `uasset refs` (free) lists what uses an asset, and
  `uasset batch` runs a file of commands at once.
- New and duplicated assets whose names end in a number (`MI_Wall_19`) load in the editor.
- Static meshes and struct properties with native serialization read correctly.
- Read Epic's template projects: formatted texts on pins, blueprints saved by UE 5.0 to 5.3, class casts.
- Faster validation (opt-in): with `UASSET_ENGINE_SPARES=N`, `validate` (and retargeting) keeps N scratch projects,
  each with an editor started ahead of the next job, which then takes seconds instead of a fresh editor's start (a
  validation about 4 s instead of 25). A waiting editor uses about 1.6 GB of memory and exits after 20 idle minutes
  (`UASSET_ENGINE_SPARE_IDLE`). Jobs that need the renderer (`render`, lighting, foliage...) still start their own
  editor. `UASSET_ENGINE_LIMIT=N` lets at most N engine jobs run at once on the machine; the others wait their turn.

## 0.1.0 – 2026-10-09

First release. Windows x64, Unreal Engine 5.8 project files.

- Read blueprints as compact text: variables, class defaults, components, widget trees, event graphs, functions,
  macros, collapsed graphs, interfaces and event dispatchers, with every wire and pin value.
- Read user-defined structs and enums, and the saved properties of any asset.
- Edit blueprints (Pro): set pin values, connect and disconnect wires, move nodes, set node comments, set variable
  defaults. Every edit is re-read and checked before it replaces the file, and the original is backed up.
- Add nodes by copying existing ones, and create new blueprints by duplicating existing ones (Pro).
- Check edits in the engine (Pro): load and compile blueprints in a headless Unreal Editor and report errors.
- Claude Code plugin with a skill that teaches Claude to use all of the above.
- Offline license keys and a 14-day Pro trial.
