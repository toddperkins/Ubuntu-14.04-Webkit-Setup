# Install Required Libraries

On a fresh Ubuntu 14.04 install, make sure you update your system.

Once the system has been updated, run the following commands from terminal:

```sh
sudo apt-get install libwebkitgtk-dev
sudo apt-get install libgtk2.0-dev
```

Create a new file called main.c and add the below code to it.

```c
#include<gtk/gtk.h>
#include<webkit/webkit.h>

int main(int argc, char** argv)
{
  GtkWidget *window;
  GtkWidget *web;
  GtkWidget *vbox;
  GtkWidget *hbox;
  GtkWidget *hbox_web_view;
  GtkWidget *go_button;
  GtkWidget *back_button;
  GtkWidget *forward_button;
  GtkWidget *stop_button;
  GtkWidget *entry;

  gtk_init(&argc,&argv);

  window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
  gtk_window_set_position(GTK_WINDOW(window), GTK_WIN_POS_CENTER);
  gtk_window_set_default_size(GTK_WINDOW(window), 850, 600);
  gtk_window_set_title(GTK_WINDOW(window), "myWebBrowser");

  vbox = gtk_vbox_new(false,false);
  hbox = gtk_hbox_new(false,false);
  hbox_web_view = gtk_hbox_new(false,false);

  gtk_container_add(GTK_CONTAINER(window), vbox);
  gtk_container_add(GTK_CONTAINER(vbox), hbox);
  gtk_container_add(GTK_CONTAINER(vbox), hbox_web_view);

  back_button = gtk_button_new_with_label("Back");
  forward_button = gtk_button_new_with_label("Forward");
  go_button = gtk_button_new_with_label("Go");
  stop_button = gtk_button_new_with_label("stop");
  entry = gtk_entry_new();
  gtk_entry_set_text (GTK_ENTRY(entry),"http://");

  gtk_box_pack_start(GTK_BOX(hbox),back_button,0,0,1);
  gtk_box_pack_start(GTK_BOX(hbox),forward_button,0,0,1);
  gtk_box_pack_start(GTK_BOX(hbox),stop_button,0,0,1);
  gtk_box_pack_start(GTK_BOX(hbox),entry,1,1,1);
  gtk_box_pack_start(GTK_BOX(hbox),go_button,0,0,0);

  web = webkit_web_view_new();
  gtk_box_pack_start(GTK_BOX(hbox_web_view),web,0,0,0);

  g_signal_connect_swapped(G_OBJECT(window), "destroy",
  G_CALLBACK(gtk_main_quit), NULL);

  gtk_widget_show_all(window);

  gtk_main();
  return 0;

}
```

Save this file, and then from a terminal execute the following command to build it.

```sh
gcc main.c -o myBrowser `pkg-config --cflags --libs gtk+-2.0 webkit-1.0`
```

To execute the browser, from terminal enter:
```sh
./myBrowser
```