1. AnimatePresence Best Practices:
```jsx
// ❌ Element disappears instantly
{isVisible && <motion.div animate={{ opacity: 1 }} />}

// ✅ Element animates out properly
<AnimatePresence>
  {isVisible && (
    <motion.div 
      key="unique-key"
      initial={{ opacity: 0 }}
      animate={{ opacity: 1 }}
      exit={{ opacity: 0 }}
    />
  )}
</AnimatePresence>
```

2. Layering for Complex Animations:
```jsx
// Like in the trash example
<Container>
  <BackLayer /> {/* Behind stuff */}
  <ContentLayer layoutId="content" /> {/* Moving content */}
  <FrontLayer /> {/* Mask or overlay */}
</Container>
```

3. Delays for Natural Sequences:
```jsx
// Stagger children
<motion.div animate={{ opacity: 1 }}>
  <motion.div animate={{ y: 0 }} transition={{ delay: 0 }} />
  <motion.div animate={{ y: 0 }} transition={{ delay: 0.1 }} />
  <motion.div animate={{ y: 0 }} transition={{ delay: 0.2 }} />
</motion.div>
```

4. Blur + Scale for Depth:
```jsx
<motion.div
  initial={{ scale: 1.1, filter: "blur(4px)", opacity: 0 }}
  animate={{ scale: 1, filter: "blur(0px)", opacity: 1 }}
  exit={{ scale: 0.9, filter: "blur(4px)", opacity: 0 }}
/>
```

5. Layout Transitions:
```jsx
// Smooth height/width changes
<motion.div layout>
  {expanded && <Content />}
</motion.div>

// Position-only for text
<motion.h1 layout="position">
  Title
</motion.h1>
```

6. Coordinated Animations with LayoutId:
```jsx
// From list to modal
<motion.div layoutId={`item-${id}`}>
  {isExpanded ? <FullContent /> : <Preview />}
</motion.div>
```

7. Mode Controls for AnimatePresence:
```jsx
// Wait for exit before enter
<AnimatePresence mode="wait">

// Pop out of layout flow during exit
<AnimatePresence mode="popLayout">
```

8. Spring Transitions for Natural Feel:
```jsx
<MotionConfig
  transition={{
    type: "spring",
    duration: 0.5,
    bounce: 0.2
  }}
>
  <App />
</MotionConfig>
```

9. Handling Complex State Sequences:
```jsx
// Like in trash example
useEffect(() => {
  if (isExiting) {
    // Sequence of state changes
    const t1 = setTimeout(() => setPhase1(true), 300)
    const t2 = setTimeout(() => setPhase2(true), 600)
    return () => {
      clearTimeout(t1)
      clearTimeout(t2)
    }
  }
}, [isExiting])
```

10. Using Custom Props for Dynamic Variants:
```jsx
<AnimatePresence custom={direction}>
  <motion.div
    custom={direction}
    variants={{
      exit: (direction) => ({
        x: direction === 'left' ? -100 : 100
      })
    }}
  />
</AnimatePresence>
```
