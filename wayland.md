wayland 实用介绍(WIP)
====================

## Wayland全局对象：
    
- wl_display：表示与服务器的连接。
- wl_registry：全局对象注册表，全局对象需要通过它获取。
- wl_compositor：窗口合成器，也是服务器。
- wl_shm：内存管理器，与窗口合成器共享内存用。
- wl_shell：支持窗口操作功能。
- wl_seat：输入设备管理器。
- wl_pointer：代表鼠标设备。
- wl_keyboard：代表键盘设备。

## wl_outputs
## wl_surfaces

## wl_display



创建wl_registry变量，通过wl_registry上获取全局变量

```c
struct wl_registry *registry = wl_display_registry(dispay);

void global_add(void *our_data, struct wl_registry *registry, uint32_t name, const char *interface, uint32_t version) {}
void global_remove(void *our_data, struct wl_registry *registry, uint32_t name) {}
struct wl_registry_listener *register_listener = { .global = global_add, .global_remove = global_remove };

void *our_data = NULL; // 我们自己的数据
wl_registry_add_listener(registry, &registry_listener, our_data);
```

## 显示流程

#### Obtain a wl_display and use it to obtain a wl_registry.
建立和wayland server之间的连接：

```c
struct wl_display *display = wl_dispay_connect(NULL);
```

- Scan the registry for globals and grab a wl_compositor and a wl_shm_pool.
- Use the wl_compositor interface to create a wl_surface.
- Use the wl_shell interface to describe your surface’s role.
- Use the wl_shm interface to allocate shared memory to store pixels in.
- Draw something into your shared memory buffers.
- Attach your shared memory buffers to the wl_surface.

[1] https://jan.newmarch.name/Wayland/index.html
[2] http://sircmpwn.github.io/2017/06/10/Introduction-to-Wayland.html
