[ ![Download](https://api.bintray.com/packages/kmdupr33/RxLoader/com.philosophicalhacker.rxloader%3Arxloader/images/download.svg) ](https://bintray.com/kmdupr33/RxLoader/com.philosophicalhacker.rxloader%3Arxloader/_latestVersion)

There's a lot of data loading solutions already for Android. I detail why I felt we needed another one [here](http://www.philosophicalhacker.com/post/rxloader-boilerplate-free-data-loading-with-loaders-and-rxjava)

`compile 'com.philosophicalhacker.rxloader:rxloader:0.1.0'`

# Basic Usage

```java
interface StoryApiService {
    Observable<List<Integer>> getStories();
}

//...

@Override
protected void onCreate(Bundle savedInstanceState) {
    storyApiService.getStories()
        .compose(RxLoader.<List<Integer>>from(this))
        .subscribeOn(Schedulers.from(AsyncTask.THREAD_POOL_EXECUTOR))
        .observeOn(AndroidSchedulers.mainThread())
        .subscribe(new Action1<List<Integer>>() {
            @Override
            public void call(List<Integer> integers) {
                Log.d(TAG, "call() called with: integers = [" + integers + "]");
            }
        }, new Action1<Throwable>() {
            @Override
            public void call(Throwable throwable) {
                Log.e(TAG, "call() called with: throwable = [" + throwable + "]");
            }
        });
}
```
