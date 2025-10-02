# Android Mobile App:

# Section 19 RecyclerView - The Grocery App

---

````
# 📱 RecyclerView in Android (Java)

A step-by-step guide to implementing **RecyclerView** in Android using Java.
RecyclerView is a modern, flexible replacement for `ListView` and `GridView`.

---

## 🔹 What is RecyclerView?

- **RecyclerView** efficiently displays large datasets by reusing (recycling) views.
- Works with:
  - **Adapter** → Supplies data to the list.
  - **ViewHolder** → Holds item views for better performance.
  - **LayoutManager** → Defines how items are arranged (list/grid/staggered).

---

## 🔹 Key Components

1. **RecyclerView** → The container for items.
2. **Adapter** → Binds data to each view.
3. **ViewHolder** → Improves scrolling efficiency.
4. **LayoutManager** → Controls item layout:
   - `LinearLayoutManager` → Vertical/Horizontal list
   - `GridLayoutManager` → Grid layout
   - `StaggeredGridLayoutManager` → Pinterest-like

---

## 🔹 Implementation Steps

### 1. Add Dependency

```
gradle
implementation 'androidx.recyclerview:recyclerview:1.3.2'
```
````

---

### 2. Add RecyclerView to Layout

```
xml
<androidx.recyclerview.widget.RecyclerView
    android:id="@+id/recyclerView"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="8dp"/>
```

---

### 3. Create Item Layout (`item_row.xml`)

```
xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:padding="12dp"
    android:orientation="horizontal">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Item Name"
        android:textSize="18sp"/>
</LinearLayout>
```

---

### 4. Create Adapter (`MyAdapter.java`)

```
java
public class MyAdapter extends RecyclerView.Adapter<MyAdapter.MyViewHolder> {

    private List<String> itemList;

    public MyAdapter(List<String> itemList) {
        this.itemList = itemList;
    }

    public static class MyViewHolder extends RecyclerView.ViewHolder {
        TextView textView;

        public MyViewHolder(View itemView) {
            super(itemView);
            textView = itemView.findViewById(R.id.textView);
        }
    }

    @NonNull
    @Override
    public MyViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext())
                .inflate(R.layout.item_row, parent, false);
        return new MyViewHolder(view);
    }

    @Override
    public void onBindViewHolder(@NonNull MyViewHolder holder, int position) {
        holder.textView.setText(itemList.get(position));
    }

    @Override
    public int getItemCount() {
        return itemList.size();
    }
}
```

---

### 5. Set Up RecyclerView in `MainActivity.java`

```
java
public class MainActivity extends AppCompatActivity {

    RecyclerView recyclerView;
    MyAdapter adapter;
    List<String> dataList;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        recyclerView = findViewById(R.id.recyclerView);
        recyclerView.setLayoutManager(new LinearLayoutManager(this));

        dataList = Arrays.asList("Apple", "Banana", "Cherry", "Mango", "Orange");
        adapter = new MyAdapter(dataList);

        recyclerView.setAdapter(adapter);
    }
}
```

---

## 🔹 Extras You Can Add

- Add **click listeners** (on tap or long press).
- Use **DiffUtil** for efficient list updates.
- Replace with **ListAdapter** for built-in DiffUtil.
- Add **ItemDecoration** for spacing/dividers.
- Implement **swipe-to-delete** or **drag-and-drop** using `ItemTouchHelper`.

---

✨ With this, you have a fully working **RecyclerView in Java**.
