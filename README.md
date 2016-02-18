# InfiniteScroll [![Build Status](https://travis-ci.org/pwittchen/InfiniteScroll.svg?branch=master)](https://travis-ci.org/pwittchen/InfiniteScroll)
[WIP] InfiniteScrollListener for RecyclerView in Android

Contents
--------
- [Motivation](#motivation)
- [Usage](#usage)
- [Example](#example)
- [Download](#download)
- [Tests](#tests)
- [Code style](#code-style)
- [Static Code Analysis](#static-code-analysis)
- [License](#license)

Motivation
----------

For a long time, I couldn't find the right implementation of the infinite scroll AKA endless scroll for Android. A few solutions I've found weren't production ready, weren't working correctly or had too many features. I wanted to have small, easy and flexible solution to implement infinite scroll for Android, which works with `RecyclerView` from the newest Android API. That's why this project was created.

Usage
-----

Create new `InfiniteScrollListener`:

```java
private InfiniteScrollListener createInfiniteScrollListener() {
  return new InfiniteScrollListener(MAX_ITEMS_PER_REQUEST, layoutManager) {
    @Override public void onScrolledToEnd(final int firstVisibleItemPosition) {
      // load your items here
      // logic of loading items will be different depending on your specific use case
      
      // when new items are loaded, combine old and new items, pass them to your adapter
      // and call refreshView(...) method from InfiniteScrollListener class to refresh RecyclerView
      refreshView(recyclerView, new MyAdapter(items), firstVisibleItemPosition);
    }
  }
}
```

Initialize `RecyclerView` and `LinearLayoutManager` in your `Activity`:

```java
public RecyclerView recyclerView;
private LinearLayoutManager layoutManager;

@Override protected void onCreate(Bundle savedInstanceState) {
  recyclerView = (RecyclerView) findViewById(R.id.recycler_view);

  layoutManager = new LinearLayoutManager(this);
  recyclerView.setHasFixedSize(true);
  recyclerView.setLayoutManager(layoutManager);
  
  // set your custom adapter
  recyclerView.setAdapter(new MyAdapter(items));
  
  // add InfiniteScrollListener as OnScrollListener
  recyclerView.addOnScrollListener(createInfiniteScrollListener());
}
```

That's it!

Example
-------

Sample app can be found in `app` directory.

Download
--------

TBD.

Tests
-----

To execute unit tests run:

```
./gradlew test
```

Code style
----------

Code style used in the project is called `SquareAndroid` from Java Code Styles repository by Square available at: https://github.com/square/java-code-styles.

Static Code Analysis
--------------------

To run Static Code Analysis, type:

```
./gradlew check
```

Reports from analysis are generated in library/build/reports/ directory.

License
-------

    Copyright 2015 Piotr Wittchen

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
    
       http://www.apache.org/licenses/LICENSE-2.0
    
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.



